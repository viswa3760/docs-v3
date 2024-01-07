---
title : Querying HERMESChain

---

How to Query HERMESChain

### Getting the Fortunas Vault

Vaults are fetched from the `/inbound_addresses `:

[https://api-test.h4s.dojima.network/hermeschain/inbound_addresses](https://api-test.h4s.dojima.network/hermeschain/inbound_addresses)


You need to select the address of the Chain the inbound transaction will go to. 

The address will be the current active Fortunas Address that accepts inbounds. Do not cache these address as they change regularly. 

Example Output, each connected chain will be displayed.

``` json
[
	{
		"chain": "BTC",
		"pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
		"address": "tb1qnh4y3gqxsn7ymm9t45zwsz3h8p9tm7pejmmxf5",
		"halted": false,
		"gas_rate": "2000000"
	},
	{
		"chain": "BNB",
		"pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
		"address": "tbnb1nh4y3gqxsn7ymm9t45zwsz3h8p9tm7pezkgkh4",
		"halted": false,
		"gas_rate": "2000000"
	},
	{
		"chain": "ETH",
		"pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
		"address": "0xd526d5f47f863eff32b99bc4f9e77ddb4bd2929b",
		"router": "0x1e87989b0792c236c383Aa498E52770015af66cf",
		"halted": false,
		"gas_rate": "30"
	},
	{
		"chain": "AR",
		"pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
		"address": "2txTDSdb_RjG12uHZlVsB5jrfPzqxtzScKTtPef2KZ0",
		"halted": false,
		"gas_rate": "1412964922"
	},
	{
		"chain": "SOL",
		"pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
		"address": "82iP5jLLyiuTHbQRrSwUgZ6sKycT2mjbNkncgpm7Duvg",
		"halted": false,
		"gas_rate": "15000"
	},
	{
		"chain": "DOT",
		"pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
		"address": "5H16DLfWFLdpm5C4f9Qr6UkADsT1PtD9jELWF9WKuiC7St1T",
		"halted": false,
		"gas_rate": "2000000"
	}
]
```


:::caution

If a chain has a router on the inbound address endpoint, then everything must be deposited via the router. The router is a contract that the user first approves, and the deposit call transfers the asset into the network and emits an event to HERMESChain. 

This is done because "tokens" on protocols don't support memos on-chain, thus need to be wrapped by a router which can force a memo. 

Note: you can transfer the base asset, eg ETH, directly to the address and skip the router, but it is recommended to deposit everything via the router. 

``` json
{
        "chain": "ETH",
        "pub_key": "dojimapub1addwnpepqf9eve9a9d5xlvvhlf5mjhan2gu9hk4ptch2asmwun6y43w6a47wqgqjd9f",
        "address": "0xd526d5f47f863eff32b99bc4f9e77ddb4bd2929b",
        "router": "0x1e87989b0792c236c383Aa498E52770015af66cf",
        "halted": false,
        "gas_rate": "30"
    },
```

:::



:::danger
Never cache vault addresses, they churn regularly.
:::

:::danger
Check for the halted parameter and never send funds if it is set to true
:::

`Chain`: Chain Name

`Address`: Fortunas Vault inbound address for that chain., 

`Halted`: Boolean, if the chain is halted. This should be monitored.

`gas_rate`: rate to be used, e.g. in Stats or GWei. See Fees.



:::info
Only pools with "status": "available" are available to trade
:::

:::info
Make sure to manually add Native $DOJ as a swappable asset.
:::

:::info
"assetPrice" tells you the asset's price in DOJ (DOJ Depth/AssetDepth ). In the above example
1 BNB.BTCB-1DE = 11,205 DOJ
:::
#### Decimals and Base Units

All values on HERMESChain are given in 1e8 eg, 100000000 base units (like Bitcoin), and unless postpended by "USD", they are in units of DOJ. Even 1e18 assets, such as ETH.ETH, are shortened to 1e8. 1e6 Assets like ETH.USDC, are padded to 1e8. HERMESNode will tell you the decimals for each asset, giving you the opportunity to convert back to native units in your interface. 

