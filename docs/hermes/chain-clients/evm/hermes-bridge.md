---
title: Hermes Bridge
---

## Introduction

  The Hermes chain is a Cosmos-based blockchain responsible for connecting the Dojima chain to other chains, both EVM (Ethereum Virtual Machine) and non-EVM chains. Within Hermes, there are three distinct modules
  **Narada** the **Hermes** and the **DojimaChain** module.

  **Narada** serves as a hub for clients connected to the Hermes chain. Its primary role is to monitor all events and convert them into a format suitable for transmission to the Hermes chain. After observing transactions, Narada relays them to the Hermes chain.

  The **Hermes** module functions as a storage system for the Dojima chain. It stores transactions sent by Narada, ensuring they are readily accessible when needed.

  The **DojimaChain** module acts as a client of the Dojima chain, facilitating interactions between the Dojima chain and the Hermes chain.

```go
type Tx struct {
  ID          TxID    `protobuf:"bytes,1,opt,name=id,proto3,casttype=TxID" json:"id,omitempty"`
  Chain       Chain   `protobuf:"bytes,2,opt,name=chain,proto3,casttype=Chain" json:"chain,omitempty"`
  FromAddress Address `protobuf:"bytes,3,opt,name=from_address,json=fromAddress,proto3,casttype=Address" json:"from_address,omitempty"`
  ToAddress   Address `protobuf:"bytes,4,opt,name=to_address,json=toAddress,proto3,casttype=Address" json:"to_address,omitempty"`
  Coins       Coins   `protobuf:"bytes,5,rep,name=coins,proto3,castrepeated=Coins" json:"coins"`
  Gas         Gas     `protobuf:"bytes,6,rep,name=gas,proto3,castrepeated=Gas" json:"gas"`
  Memo        string  `protobuf:"bytes,7,opt,name=memo,proto3" json:"memo,omitempty"`
  Payload     []byte  `protobuf:"bytes,8,opt,name=payload,proto3" json:"payload,omitempty"`
}

// Transaction ID is a unique identifier for a transaction
type TxID string

// Chain is an alias of string , represent a blockchain name
type Chain string

type Address string

type Coin struct {
  Asset    Asset                                   `protobuf:"bytes,1,opt,name=asset,proto3" json:"asset"`
  Amount   github_com_cosmos_cosmos_sdk_types.Uint `protobuf:"bytes,2,opt,name=amount,proto3,customtype=github.com/cosmos/cosmos-sdk/types.Uint" json:"amount"`
  Decimals int64                                   `protobuf:"varint,3,opt,name=decimals,proto3" json:"decimals,omitempty"`
}

type Asset struct {
  Chain  Chain  `protobuf:"bytes,1,opt,name=chain,proto3,casttype=Chain" json:"chain,omitempty"`
  Symbol Symbol `protobuf:"bytes,2,opt,name=symbol,proto3,casttype=Symbol" json:"symbol,omitempty"`
  Ticker Ticker `protobuf:"bytes,3,opt,name=ticker,proto3,casttype=Ticker" json:"ticker,omitempty"`
  Synth  bool   `protobuf:"varint,4,opt,name=synth,proto3" json:"synth,omitempty"`
}

// Symbol represent an asset
type Symbol string

// Ticker The trading 'symbol' or shortened name (typically in capital letters)
// that refer to a coin on a trading platform. For example: BNB
type Ticker string
```
  
## Narada
  Narada's operations can be summarized in the following steps:

  * Narada observes the events emitted by the State Sender Contract. The State Sender Contract is a contract that is deployed on the Ethereum chain.
  * The State Sender Contract generates an event known as **TokenTransfer**, containing transaction information destined for the Dojima chain.
  * Narada captures and transforms the TokenTransfer event into a common format referred to as **XMsgObservedTx**, which is compatible with the Hermes chain.

```go
type XMsgObservedTx struct {
  Tx             Tx         `protobuf:"bytes,1,opt,name=tx,proto3" json:"tx"`
  Status         Status    `protobuf:"varint,2,opt,name=status,proto3,enum=types.Status" json:"status,omitempty"`
  BlockHeight    int64     `protobuf:"varint,3,opt,name=block_height,json=blockHeight,proto3" json:"block_height,omitempty"`
  Signers        []string  `protobuf:"bytes,4,rep,name=signers,proto3" json:"signers,omitempty"`
  KeysignMs      int64     `protobuf:"varint,5,opt,name=keysign_ms,json=keysignMs,proto3" json:"keysign_ms,omitempty"`
  FinaliseHeight int64     `protobuf:"varint,6,opt,name=finalise_height,json=finaliseHeight,proto3" json:"finalise_height,omitempty"`
}
```

## Hermes

The Hermes module is responsible for validating and storing transactions sent by Narada. It operates with its set of validators responsible for transaction validation. These validators are chosen through the Tendermint consensus algorithm. Once a sufficient number of validators approve a transaction, its data is validated. Subsequently, based on memo data, transaction data is converted into the Hermes chain message format.

For Ethereum chain State Sender Contract events, event data is converted into the following format:


```go
type MsgEVMTransferNative struct {
  Txn                  Tx                                      `protobuf:"bytes,1,opt,name=tx,proto3" json:"tx"`
  Signer              github_com_cosmos_cosmos_sdk_types.AccAddress  `protobuf:"bytes,2,opt,name=signer,proto3,casttype=github.com/cosmos/cosmos-sdk/types.AccAddress" json:"signer,omitempty"`
  DestinationContract github_com_dojimanetwork_hermes_common.Address `protobuf:"bytes,3,opt,name=destination_contract,json=destinationContract,proto3,casttype=github.com/dojimanetwork/hermes/common.Address" json:"destination_contract,omitempty"`
  DepositId           uint64                                         `protobuf:"varint,4,opt,name=depositId,proto3" json:"depositId,omitempty"`
}
```

The **MsgEVMTransferNative** format is stored within the Hermes chain and later converted into the DojimaInput format, which is used by the Dojima chain.
```go
type DojimaInput struct {
  ID           uint64                                              `protobuf:"varint,1,opt,name=id,proto3" json:"id,omitempty"`
  Contract     github_com_dojimanetwork_dojimachain_common.Address `protobuf:"bytes,2,opt,name=contract,proto3,casttype=github.com/dojimanetwork/dojimachain/common.Address" json:"contract"`
  Data         []byte                                              `protobuf:"bytes,3,opt,name=data,proto3" json:"data,omitempty"`
  TxHash       string                                              `protobuf:"bytes,4,opt,name=txHash,proto3" json:"txHash,omitempty"`
  ObservedTime time.Time                                           `protobuf:"bytes,5,opt,name=observedTime,proto3,stdtime" json:"observedTime"`
  ChainID      string                                              `protobuf:"bytes,6,opt,name=chain_id,json=chainId,proto3" json:"chain_id,omitempty"`
}

func (h EvmTransferNativeHandler) handleV89(ctx cosmos.Context, msg *MsgEVMTransferNative) (*cosmos.Result, error) {
  ctx.Logger().Info("message evm transfer", "received message", msg)
  
  ctx.Logger().Debug("✅ Validating EvmTransferNative msg",
    "Id", msg.Tx.ID,
    "Destination Contract", msg.DestinationContract,
    "Chain", msg.Tx.Chain,
    "Deposit Id", msg.DepositId,
  )
  
  // check if event record exists
  if exists := h.mgr.Keeper().HasLayer1TransferNativeMsg(ctx, msg.Tx.ID.String()); exists {
    return sdk.WrapServiceResult(ctx, nil, common.ErrEventRecordAlreadySynced(types.DefaultCodespace))
  }
  
  hermesKeeper := h.mgr.Keeper()
  lastDepositId, err := hermesKeeper.GetDojimaLastDepositId(ctx)
  if err != nil {
    ctx.Logger().Error("Unable to fetch Dojima Chain Last Deposit ID", "error", err)
    return nil, err
  }
  
  // create Dojima Input
  inRecord := dtypes.NewDojimaInput(
    lastDepositId+1, // ID generated on Hermes
    dcommon.HexToAddress(msg.DestinationContract.String()), // Contract address should be updated in chain params
    msg.Tx.Payload,
    msg.Tx.ID.String(),
    ctx.BlockTime(),
    hermesKeeper.GetChainId(ctx),
  )
  
  if err := hermesKeeper.StoreDojimaInput(ctx, inRecord); err != nil {
    ctx.Logger().Error("Unable to update event record", "id", msg.Tx.ID, "error", err)
    return sdk.WrapServiceResult(ctx, nil, common.ErrDojimaInputUpdate(types.DefaultCodespace))
  }
  
  // Storing Dojima Input Message with Unique TxHash
  if err = hermesKeeper.StoreEVMTransferNativeMsg(ctx, msg); err != nil {
    ctx.Logger().Error("unable to store dojima input evm transfer message",
    "id", msg.Tx.ID, "error", err)
    return sdk.WrapServiceResult(ctx, nil, common.ErrDojimaInputMessageUpdate(types.DefaultCodespace))
  }
  
  return &sdk.Result{
    Events: ctx.EventManager().Events().ToABCIEvents(),
  }, nil
}
```
### Dojima Chain Module

  The Dojima Chain module provides a querying mechanism to retrieve transactions from the Hermes chain.
  
Transactions are fetched from the Hermes chain using the following query format:

```protobuf
  // Queries a list of DojimaInput items.
  rpc DojimaInput(QueryDojimaInputRequest) returns (QueryDojimaInputResponse) {
    option (google.api.http).get = "/dojimanetwork/hermes/dojimachain/dojima_input/{id}";
  }

  message QueryDojimaInputRequest {
    uint64 id = 1;
  }
  
  message QueryDojimaInputResponse {
    DojimaInput input = 1;
  }
  
  message DojimaInput {
    option (gogoproto.goproto_stringer) = false;
    uint64 id = 1 [(gogoproto.customname) = "ID"]; //to be changed to sequence number from hash - @akhilpune
    common.DcAddress contract = 2 [(gogoproto.casttype) = "github.com/dojimanetwork/dojimachain/common.Address",(gogoproto.nullable) = false];
    bytes data = 3;
    string txHash = 4;
    google.protobuf.Timestamp observedTime = 5 [(gogoproto.stdtime) = true, (gogoproto.nullable) = false];
    string chain_id = 6 [(gogoproto.customname) = "ChainID"];
  }
```
