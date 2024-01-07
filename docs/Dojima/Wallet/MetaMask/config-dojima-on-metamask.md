---
title: Add Dojima Network
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

In order to view the flow of funds in your accounts, on the Dojima Network, you will need to configure Dojima `{testnet, mainnet}` URL on Metamask.

There are two ways to do it:
1. [Using Dojimascan](developers/wallet/metamask/config-dojima-on-metamask.md#using-dojima-scan)
2. [Add the Dojima network manually](developers/wallet/metamask/config-dojima-on-metamask.md#add-the-dojima-network-manually)
### Using Dojimascan

:::note
Please make sure you have already installed <ins>**[Metamask](https://metamask.io/)**</ins>!
:::


<Tabs
  defaultValue="mainnet"
  values={[
    { label: 'Dojima-Testnet', value: 'mainnet', },
  ]
}>

<TabItem value="mainnet">

Please follow the steps to add Dojima’s Testnet:

- Navigate to [https://doj-bex-test.dojima.network/](https://doj-bex-test.dojima.network/)

<img src={useBaseUrl("https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/block_testnet.jpeg")} />
<p></p>

- Scroll down to the bottom of the page and click on the button `Add Dojima Network`

<img src={useBaseUrl("https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/add_network.png")} width="357" height="600" />

- Once you click the button you will see a Metamask Notification, now click on **Approve**.
You will be directly switched to Dojima’s Testnet now in the network dropdown list. You can now close the dialog.

</TabItem>

</Tabs>

If you are facing any issue, **Add the Network Manually(steps given below)**

### Add the Dojima network manually

<Tabs
  defaultValue="mainnet"
  values={[
    { label: 'Dojima-Testnet', value: 'mainnet', },
  ]
}>
<TabItem value="mainnet">
To add Dojima’s Testnet, click on the Network selection dropdown and then click on Custom RPC.

<img src={useBaseUrl("https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/metamask/select-network.png")} />

It will open up a form with 2 tabs on the top, Settings and Info. In the Settings tab you can add `Dojima Testnet` in the Network Name field, URL `https://api-test.d11k.dojima.network:8545/` in the New RPC URL field, `1001` in Chain ID field, `DOJ` in Currency Symbol field and `https://doj-bex-test.dojima.network/` in Block Explorer URL field.

<img src={useBaseUrl("https://dojima-images.s3.ap-south-1.amazonaws.com/dojima-docs/img/metamask/testnet-add-network.png")} width="357" height="600" />

Once you’ve added the information click on Save. You will be directly switched to Dojima’s Testnet now in the network dropdown list. You can now close the dialog.
</TabItem>
</Tabs>

**You have successfully added Dojima Network to your Metamask!**
