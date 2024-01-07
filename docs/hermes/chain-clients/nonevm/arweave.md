---
title: Arweave Chain Client
---

## Introduction

Arweave is a new type of storage that backs data with sustainable and perpetual endowments, allowing users and developers to truly store data forever – for the very first time.

As a collectively owned hard drive that never forgets, Arweave allows us to remember and preserve valuable information, apps, and history indefinitely. By preserving history, it prevents others from rewriting it.

## Scanning Blocks

The block scanner monitors fortuna addresses and looks for incoming transactions to those addresses. When it sees, it performs validations and witnesses to hermes chain.

```go
      txInfo, err := c.client.GetTransactionByID(tx)
	  
      // if tx is not found, invalid
      if err == argo.ErrNotFound || err == argo.ErrInvalidId {
      return types.TxInItem{}, err
      }
      
      // converting signature data to owner address
      sender, err := arutils.OwnerToAddress(txInfo.Owner)
      
      if err != nil {
      return types.TxInItem{}, err
      }
      
      winstonQtyStr := txInfo.Quantity
      winstonFeeStr := txInfo.Reward
      
      winstonQty, ok := cosmos.ParseUint(winstonQtyStr)
      
      if ok != nil {
      err = fmt.Errorf("invalid amount: %v", winstonQtyStr)
      return types.TxInItem{}, err
      }
      
      _, ok = cosmos.ParseUint(winstonFeeStr)
      
      if ok != nil {
      err = fmt.Errorf("invalid fee: %v", winstonFeeStr)
      return types.TxInItem{}, err
      }
      
      // when value is less than or equal to zero, it is data transaction not a transfer
      if winstonQty.IsZero() {
      return types.TxInItem{}, fmt.Errorf("not a transfer transaction, its a data transaction, so ignoring")
      }
	  
      client := argo.NewClient("https://arweave.net")
      address := os.Getenv("AR_ADDRESS")
      reward, err := client.GetTransactionPrice([]byte(""), &address)
      convReward := cosmos.NewUint(uint64(reward))
      // till here
      
      if err != nil {
      c.logger.Error().Err(err).Msg("failed to get arweave fee")
      }
      
      gasFee := common.Gas{
      common.NewCoin(common.ARAsset, convReward).WithDecimals(common.ARWEAVECHAIN.GetGasAssetDecimal()),
      }
      // update memory cache
      c.udpateARGasCache(convReward)
      
      toAddr := txInfo.Target
      
      //read memo from tags [{name, value}]
      var memo string
      for _, val := range txInfo.Tags {
      if strings.EqualFold(val.Name, "memo") {
      memo = val.Value
      c.logger.Debug().Str("memo", memo).Msg("found memo field")
      }
      }
      
      if memo == "" {
      c.logger.Debug().Str("memo", memo).Msg("found empty memo")
      }
      
      return types.TxInItem{
      BlockHeight: height,
      Tx:          txInfo.ID,
      Sender:      sender,
      To:          toAddr,
      Coins: common.Coins{
      common.NewCoin(common.ARAsset, winstonQty).WithDecimals(common.ARWEAVECHAIN.GetGasAssetDecimal()),
      },
      Memo: memo,
      Gas:  gasFee,
      }, nil
```

## Arweave Signer

Signer works on signing the outbound transactions received txout from hermes chain that needs to sent on arweave chain. Signing transactions are done in two ways: using rsa tss signing algo and single wallet signing.

```go

      _, err := tx.VaultPubKey.GetAddress(c.GetChain())
      //c.logger.Debug().Msgf("process outbound tx", fromAddr)
      if err != nil {
      return &types.Transaction{}, fmt.Errorf("failed to convert arweave address (%s): %w", tx.VaultPubKey.String(), err)
      }
      
      // initialise to collect all received txout substractFee coins
      var coins = cosmos.NewUint(0)
      for _, coin := range tx.Coins {
      // handle sors return, leave enough coin to pay for gas.
      if strings.HasPrefix(tx.Memo, hermes.TxToStringMap[hermes.TxSorsReturn]) {
      if coin.Asset == c.cfg.ChainID.GetGasAsset() {
      substractFee := c.averageFee().Mul(cosmos.NewUint(3)).Quo(cosmos.NewUint(2))
      if coin.Amount.LT(substractFee) {
      return &types.Transaction{}, fmt.Errorf("not enough to pay for transaction, Origal amount %d, Fee %d", coin.Amount.Uint64(), substractFee.Uint64())
      }
      
      coin.Amount = coin.Amount.Sub(substractFee)
      }
      }
      coins = coins.Add(coin.Amount)
      }
      
      tag := types.Tag{
        Name:  "memo",
        Value: tx.Memo,
      }
      
      var tags []types.Tag
      tags = append(tags, tag)
      encodeTag := utils.TagsEncode(tags)
      
      arTx := &types.Transaction{
      Format:   2,
      Quantity: coins.String(),
      Data:     "",
      DataSize: "0",
      Reward:   c.averageFee().String(),
      Target:   tx.ToAddress.String(),
      Tags:     encodeTag,
      }
  	
      return arTx, nil
```