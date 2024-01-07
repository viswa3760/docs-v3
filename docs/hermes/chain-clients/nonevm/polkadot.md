---
title: Polkadot Chain Client
---

## Introduction

  Polkadot unites and secures a growing ecosystem of specialized blockchains called parachains. Apps and services on Polkadot can securely communicate across chains, forming the basis for a truly interoperable decentralized web.

## Scanning Blocks

  The block scanner monitors fortuna addresses and looks for incoming transactions to those addresses. When it sees, it performs validations and witnesses to hermes chain.

```go
    func (c *Client) convertToTxIn(dextrinsic *DecodedExtrinsic, height int64) (types.TxInItem, error) {
      e := dextrinsic.Extrinsic
      call, ok := e.Metadata.CallIndex[e.CallIndex]
      if !ok {
        return types.TxInItem{}, fmt.Errorf("failed to get call index from metadata")
      }
      // if extrinsic module is utility and function is batch all or batch with signed tx, gas class is normal
      // https://docs.substrate.io/build/tx-weights-fees/
      if e.Module == "Utility" && (call.Call.Name == "batch_all" || call.Call.Name == "batch") && e.ContainsTransaction && len(e.Signature) > 0 && dextrinsic.PaymentInfo.Class == "normal" {
        dest := " "
        dotQty := cosmos.ZeroUint()
        memo := ""
        calls := &[]UtilityBatchCall{}
        err := unmarshalAny(calls, e.Params[0].Value)
        gas := dextrinsic.PaymentInfo.PartialFee.BigInt().Uint64()
        comsosGas := cosmos.NewUint(gas)
        c.updateDOTGasCache(comsosGas)
        if err != nil {
          return types.TxInItem{}, err
        }
    
        for _, c := range *calls {
          for _, a := range c.Params {
            switch a.Name {
            // decode destination address to ss58
            case "dest":
              dest = EncodeToSS58(a.Value.(map[string]interface{})["Id"].(string))
              break
              // get transacted value to dest address
            case "value":
              value := a.Value.(string)
              dotQty, err = cosmos.ParseUint(value)
              if err != nil {
                return types.TxInItem{}, err
              }
              break
              // get memo field
            case "remark":
              memoBeforeConv := a.Value.(string)
              parts := strings.Split(memoBeforeConv, ":")
              if len(parts) < 2 {
                return types.TxInItem{}, fmt.Errorf("invalid memo of dot transaction %s, tx hash %s", memo, e.ExtrinsicHash)
              }
              if strings.EqualFold(parts[0], "memo") {
                memo = strings.Join(parts[1:], ":")
              } else {
                return types.TxInItem{}, fmt.Errorf("invalid memo of dot transaction %s, tx hash %s", memo, e.ExtrinsicHash)
              }
              break
            }
          }
        }
    
        return types.TxInItem{
          BlockHeight: height,
          Tx:          e.ExtrinsicHash,
          Sender:      EncodeToSS58(e.Address.(string)),
          To:          dest,
          Memo:        memo,
          Coins: common.Coins{
            common.NewCoin(common.DOTAsset, dotQty).WithDecimals(common.DOTCHAIN.GetGasAssetDecimal()),
          },
          Gas: common.Gas{
            common.NewCoin(common.DOTAsset, comsosGas).WithDecimals(common.DOTCHAIN.GetGasAssetDecimal()),
          },
        }, nil
      }
    
      return types.TxInItem{}, nil
    }
```

## Polkadot Signer

Signer works on signing the outbound transactions received txout from hermes chain that needs to sent on arweave chain. Signing transactions are done in two ways: using ed25519/sr25519 tss signing algo and single wallet signing.

```go
    func (c *Client) processOutboundTx(tx stypes.TxOutItem, hermeschainHeight int64) (gsrpcTypes.SignatureOptions, gsrpcTypes.Extrinsic, error) {
      _, err := tx.VaultPubKey.GetAddress(c.GetChain())
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, fmt.Errorf("failed to convert polkadot address (%s): %w", tx.VaultPubKey.String(), err)
      }
    
      // initialise to collect all received txout substractFee coins
      var coins = cosmos.NewUint(0)
      for _, coin := range tx.Coins {
        // handle sors return, leave enough coin to pay for gas.
        if strings.HasPrefix(tx.Memo, hermes.TxToStringMap[hermes.TxSorsReturn]) {
          if coin.Asset == c.cfg.ChainID.GetGasAsset() {
            substractFee := c.averageFee().Mul(cosmos.NewUint(3)).Quo(cosmos.NewUint(2))
            if coin.Amount.LT(substractFee) {
              return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, fmt.Errorf("not enough to pay for transaction, Origal amount %d, Fee %d", coin.Amount.Uint64(), substractFee.Uint64())
            }
    
            coin.Amount = coin.Amount.Sub(substractFee)
          }
        }
        coins = coins.Add(coin.Amount)
      }
    
      // fetch the latest metadata from chain
      metadata, err := c.GetLatestMetadata()
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // convert from ss58 to hexadecimal address
      hexAddr := DecodeFromSS58(tx.ToAddress.String())
      appendX := strings.Join([]string{"0x", hexAddr}, "")
      dest, err := gsrpcTypes.NewMultiAddressFromHexAccountID(appendX)
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // append memo string to tx.memo and join with ":"
      memoArray := strings.Join([]string{"memo", tx.Memo}, ":")
      memo := []byte(memoArray)
    
      // prepare system::remark call
      remarkCall, err := gsrpcTypes.NewCall(metadata, "System.remark", memo)
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // dest amount
      valUint64 := coins.Uint64()
      amount := gsrpcTypes.NewUCompactFromUInt(valUint64)
    
      // prepare balances::transfer call
      transferCall, err := gsrpcTypes.NewCall(metadata, "Balances.transfer", dest, amount)
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // prepare utility::batch_all
      utilityBatchCall, err := gsrpcTypes.NewCall(metadata, "Utility.batch_all", []gsrpcTypes.Call{transferCall, remarkCall})
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // fetch genesis hash for immortal era.
      genesisHash, err := c.gsrpc.RPC.Chain.GetBlockHash(0)
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // create storage key
      storageKey, err := gsrpcTypes.CreateStorageKey(metadata, "System", "Account", c.dotKeysignWrapper.dotKP.PublicKey)
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // fetch account info for nonce value
      var accountInfo gsrpcTypes.AccountInfo
      ok, err := c.gsrpc.RPC.State.GetStorageLatest(storageKey, &accountInfo)
      nonce := accountInfo.Nonce
    
      if err != nil || !ok {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // fetch runtime version data
      runtimeVersion, err := c.GetRuntimeVersion()
    
      if err != nil {
        return gsrpcTypes.SignatureOptions{}, gsrpcTypes.Extrinsic{}, err
      }
    
      // prepare extrinsic for signing
      extrinsic := gsrpcTypes.NewExtrinsic(utilityBatchCall)
    
      return gsrpcTypes.SignatureOptions{
        BlockHash:          genesisHash,
        Era:                gsrpcTypes.ExtrinsicEra{IsMortalEra: false},
        GenesisHash:        genesisHash,
        Nonce:              gsrpcTypes.NewUCompactFromUInt(uint64(nonce)),
        SpecVersion:        runtimeVersion.SpecVersion,
        Tip:                gsrpcTypes.NewUCompactFromUInt(0),
        TransactionVersion: runtimeVersion.TransactionVersion,
      }, extrinsic, nil
    }
```