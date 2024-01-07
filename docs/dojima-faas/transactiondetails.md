---
title : Transaction Details
---

**Returns transaction details such as detailed transaction data, transactions history based on mentioned token, network and related data.**

## History

**Returns list of transactions done by an address based on respective token input and network.**

### GET Arweave

```

https://faas-test.dojima.network/dojima-faas/v1/txs/history/arweave?address=iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys&network=mainnet

```

**Returns list of transactions done by an address for arweave.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Public address of the respective tokens were generated:


    - Bitcoin
    - Arweave
    - Ethereum
    - Solana 


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**address**   |  **Required:** Public address of the user to which transactions history to be displayed.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |
| **limit** | Optional. Default 100. Number of transactions to be displayed per call. |

### Example Request and Response

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
https://faas-test.dojima.network/dojima-faas/v1/txs/history/arweave?address=iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys&network=mainnet
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "******************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/txs/history/arweave?address=iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys&network=mainnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "outer": [
    {
      "timestamp": 1648533262,
      "transaction_hash": "sAn6BS_kQXYO2tq9NdNcQInzQBy8ai05T1lIoLVOFSE",
      "block": 902207,
      "from": "iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys",
      "to": "4JOmaT9fFe2ojFJEls3Zow5UKO2CBOk7lOirbPTtX1o",
      "value": "0.212303132894",
      "gas_price": "0.000000724176",
      "date": "29/03/2022",
      "time": "11:24:22"
    },
    {
      "timestamp": 1648520642,
      "transaction_hash": "UygVPWgsvFYJnie_VmFXq4sXkq_48AxMQ2AuGTWWwVM",
      "block": 902106,
      "from": "iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys",
      "to": "4JOmaT9fFe2ojFJEls3Zow5UKO2CBOk7lOirbPTtX1o",
      "value": "263.746368279452",
      "gas_price": "0.000000731880",
      "date": "29/03/2022",
      "time": "07:54:02"
    }
  ],
  "inner": [
    {
      "timestamp": 1648533262,
      "transaction_hash": "sAn6BS_kQXYO2tq9NdNcQInzQBy8ai05T1lIoLVOFSE",
      "block": 902207,
      "from": "iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys",
      "to": "4JOmaT9fFe2ojFJEls3Zow5UKO2CBOk7lOirbPTtX1o",
      "value": "0.212303132894",
      "gas_price": "0.000000724176",
      "date": "29/03/2022",
      "time": "11:24:22",
      "signature": "FTALC7RxZVXkd1cETUl83Zt8ZV-zOfy2lqPpC8XzKdzcu_pLBGCdq-UNT-YMfgiurPm4Tt673p7VgudNu55Lu76njnFi2oqnK7Ixn9pp3oMZVtNFEFf3u_MILeRC45arkzFUhZkPDRJkvHIDiKvDKHF1fUkJw20Eg0EiCZTjlkm7g-Uw3vHdESEwNVUv8O43Hg60yvk3Ky8c7k-blVxoD1GRcmLiayLoYRbpYLYyiyYgHZXkdeXLDll2DVjnjVT8RaQqG_EBlZRMkMKHX-FLmwFwmA0nM9PSaz9jQqk8ostxB_Qyl8lsTJ4UzviPfi8MS_f66s6vCL1_JOg2aBiyVTjy_d_Xk6LS7K6T8-5wtuJsz7TTSFzmSsrkrpMap1t2RDmzbNdYiTna0S0CAVWtoS8pZOr_MxUpfvEvrFrcS_EJfg37XzWnT5djVZGcpIs9xYGCechoH6t6Vptn4hYgBBmxUbPfl_LiCU0qevJeyd6rNbg-_23tX7owRUR1GzLBov2o4FRI5A2A2xuP6unNdLWoXOSc0DY5rupToQbj4DjYK1cbeCbvJcGi6MadRaxSRushhRyhhF1ugdwOj7VRPw_m41VR1pm5S4MWuPIWnSUNDgULkFRKKs4XUJLmon77AHlDHvymYVuNFEBXmoWdcvqakcsq60D7irlsmmFiyyg",
      "block_hash": "LUIt2kLzASel09V0VhYQWd4cyrNtTW_QVqOXakuuIZLALWE87t88LQjCZl9aA9XV"
    },
    {
      "timestamp": 1648520642,
      "transaction_hash": "UygVPWgsvFYJnie_VmFXq4sXkq_48AxMQ2AuGTWWwVM",
      "block": 902106,
      "from": "iy3E3sNIM42BPCMIUYns7YZVeNr9Fphg3EjtAxidXys",
      "to": "4JOmaT9fFe2ojFJEls3Zow5UKO2CBOk7lOirbPTtX1o",
      "value": "263.746368279452",
      "gas_price": "0.000000731880",
      "date": "29/03/2022",
      "time": "07:54:02",
      "signature": "fLsUf_CNzFi2uRje-L4lRd2d4uDAuoZkml9XUn4dyZ4aPsEQZHOMPLuwT3w2nubO0PHvIdPPNPmvjQtcCsc9BIhjXPJWNT3mig03l9s66x1BWaikkbKPYhQ5AF457AhEwqVkXTDARMWSURc3rbjhCAzeHwnwNGmkDd9CS3OGLwfboJa_MArbArzIgz80cuBZ6LCtAWz1xzZ_4TZycKrbhhrXpjeGkYrYxpNJSSK8gaKJTnln2Nb24JkprNtSJtTnmdrg4_iyDbHyj2kYopDtNXOhwx2Q6QqjgmxRC35z5F-QqCwlzJRBQsNkNNEjsszI4klfenQCa9slnCukPuPW1gVzV6RmzYcXApHL_M8ZSF38qCMok67qhbPAnl0psv1Vkz9lXBTixA26UVg4fJRALGxsu5jp3dxbKmZCDWZciSXctjjYj1CAyXcPY-UDkdWleOAAKUFUvfs8G2S9JeNwO-g3J_VOticujYgB6Aypac8LJFAiBpRAZP8tspqsZBDXxw3X0u9s3mk715mIWLDExhg6D38LD75Ve2XeM1iDEJ19DBfeom3kHoX3gP3NPIYMuPqMw1b9nliTQGBNkswP-kNqurGLooiFh_vKQsRKCeHeN1sdiaaVGKZ6DteEEl7ETcWZPh3Grmi0gDVexWj7_prnGCBtESMKCkkAlY5UyNg",
      "block_hash": "6hC5-XX2FQYHNgxx_2_fXGLF8rOt5JJXify0CJk2NzzeXrNKB_B_6HJn1RKH0Fpi"
    }
  ]
}

```


```mdx-code-block
</TabItem>

</Tabs>
```

### GET Bitcoin

```

https://faas-test.dojima.network/dojima-faas/v1/txs/history/bitcoin?address=tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp&network=testnet

```

**Returns list of transactions done by an address for bitcoin.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Public address of the respective tokens were generated:


    - Bitcoin
    - Arweave
    - Ethereum
    - Solana 


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**address**   |  **Required:** Public address of the user to which transactions history to be displayed.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |

### Example Request and Response



```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/txs/history/bitcoin?address=tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp&network=testnet' \
--header 'X-API-KEY: ****************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "****************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/txs/history/bitcoin?address=tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp&network=testnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "txs": [
    {
      "transaction_hash": "8f035c2dbfbf459e34a9d480d1881095225c9d0801901b9387f2cd4b7533f16b",
      "block": 2311311
    },
    {
      "transaction_hash": "f51dd2de32005d1289feef06d1ae37da08611f4755210ac8f3545a4cd9de27d8",
      "block": 2287294
    },
    {
      "transaction_hash": "86809c56e572ec254a87fe3eafa8acc44b9d380dce7677f95662a6901034e071",
      "block": 2286923
    },
    {
      "transaction_hash": "d5b0fe15206e3895222b9453891b625b5fa0847cb138d5e43755aac770de9b39",
      "block": 2286923
    },
    {
      "transaction_hash": "6f8f8ace22a5f20582b26d64f9fabf964af2001350cab8379ef86d4b58649732",
      "block": 2286587
    },
    {
      "transaction_hash": "5529b297e8d29bfbb1b5916ae8dca461d852a17f88d5fa78828314830c3007db",
      "block": 2285931
    },
    {
      "transaction_hash": "2a2731428b3bd122d214e65e68521f88342463f02a11d612c682b4e49387f116",
      "block": 2285906
    }
  ]
}
```


```mdx-code-block
</TabItem>

</Tabs>
```

### GET Ethereum

```

https://faas-test.dojima.network/dojima-faas/v1/txs/history/ethereum?address=0x0577e1E35C4f30cA8379269B7Fd85cBCE7F084f4&network=testnet
```

**Returns list of transactions done by an address for ethereum.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Public address of the respective tokens were generated:


    - Bitcoin
    - Arweave
    - Ethereum
    - Solana 


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**address**   |  **Required:** Public address of the user to which transactions history to be displayed.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |
| **limit** | Optional. Default 100. Number of transactions to be displayed per call. |
| **sort**  | Optional. Default 'desc'. Display of transactions order asc or desc. |
| **startBlock** | Optional. Default 0. Start block number to display transactions from. |
| **endBlock**   | Optional. Default 99999999. End block number to display transactions until. |
| **page**       | Optional. Default 1. Transactions page number. |

### Example Request and Response



```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/txs/history/bitcoin?address=tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp&network=testnet' \
--header 'X-API-KEY: ****************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "****************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/txs/history/bitcoin?address=tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp&network=testnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "txs": [
    {
      "transaction_hash": "8f035c2dbfbf459e34a9d480d1881095225c9d0801901b9387f2cd4b7533f16b",
      "block": 2311311
    },
    {
      "transaction_hash": "f51dd2de32005d1289feef06d1ae37da08611f4755210ac8f3545a4cd9de27d8",
      "block": 2287294
    },
    {
      "transaction_hash": "86809c56e572ec254a87fe3eafa8acc44b9d380dce7677f95662a6901034e071",
      "block": 2286923
    },
    {
      "transaction_hash": "d5b0fe15206e3895222b9453891b625b5fa0847cb138d5e43755aac770de9b39",
      "block": 2286923
    },
    {
      "transaction_hash": "6f8f8ace22a5f20582b26d64f9fabf964af2001350cab8379ef86d4b58649732",
      "block": 2286587
    },
    {
      "transaction_hash": "5529b297e8d29bfbb1b5916ae8dca461d852a17f88d5fa78828314830c3007db",
      "block": 2285931
    },
    {
      "transaction_hash": "2a2731428b3bd122d214e65e68521f88342463f02a11d612c682b4e49387f116",
      "block": 2285906
    }
  ]
}
```

```mdx-code-block
</TabItem>

</Tabs>
```
### GET Solana

```

https://faas-test.dojima.network/dojima-faas/v1/txs/history/solana?address=DxehLnrWp8iP5ahoG413BD4azVrkgA8Pob4rXco3mpCS&network=devnet
```

**Returns list of transactions done by an address for solana.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Public address of the respective tokens were generated:

    - Bitcoin
    - Arweave
    - Ethereum
    - Solana 


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**address**   |  **Required:** Public address of the user to which transactions history to be displayed.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |
| **offset** | Optional. Default 100. Number of transactions to be displayed per call. |
| **beforeHash**  | Optional. Default null. Search list of txs backwards before hash |
| **untilHash** | Optional. Default null. Search list of txs until hash |

### Example Request and Response



```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/txs/history/solana?address=DxehLnrWp8iP5ahoG413BD4azVrkgA8Pob4rXco3mpCS&network=devnet' \
--header 'X-API-KEY: *********************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "*********************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/txs/history/solana?address=DxehLnrWp8iP5ahoG413BD4azVrkgA8Pob4rXco3mpCS&network=devnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "txs": [
    {
      "transaction_hash": "PGgVXU6HCwtQf6td5niURcYtNHru4YWZgWBNBBS1pg2uUcSwcBEUFUTqmNaFbMCdbKfsqTPCwG7CHmKquoeREsH",
      "block": 150376165,
      "date": "25/07/2022",
      "time": "14:17:52"
    },
    {
      "transaction_hash": "2eYrMHzEHVtGf5XtCfvzi3NFNXA4o8tmH8UBUrE4pPT9VigWHtXo7ttDAbTWjJp3mDan7cuBW5BtCV2UD1Nzn684",
      "block": 149736491,
      "date": "22/07/2022",
      "time": "18:51:56"
    },
    {
      "transaction_hash": "2irwfmujx2BWsWEWfwcXwV3dZqoiYtn7HMNBF13z33QngNpF1JiifsE3Nuw6gJKxBbpERhf2WLpdg2ZfDE2EevU2",
      "block": 149428445,
      "date": "21/07/2022",
      "time": "10:21:40"
    },
    {
      "transaction_hash": "3ZAhtNmTtx4vXFYmPqKbVZrgHaydhrFPZ8TGFZvLfh9SMrooVyEtXVrADidgt7kHVFRZQtMctA4yqmz5kLRR5EDa",
      "block": 149317976,
      "date": "20/07/2022",
      "time": "22:42:38"
    },
    {
      "transaction_hash": "3Gof6XhyeqgEW3wYV7DZCixom4zmRn3n6idn95fHJtWV1EAi3zP2cWq7AfRvfRpkDMmbA1FGm3bf6mMC411Yhhy5",
      "block": 149260715,
      "date": "20/07/2022",
      "time": "16:39:47"
    }
  ]
}
```

```mdx-code-block
</TabItem>

</Tabs>
```

## Hash data

**Returns transaction details by hash based on respective token and network.**

### GET Arweave

```

https://faas-test.dojima.network/dojima-faas/v1/tx/data/arweave?hash=3NDXWouOXjWCVAkdIbjXTw91SNVRljwHiMoR3IavEac&network=mainnet
```

**Returns transaction details by hash for arweave.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**hash**   |  **Required.** Transaction hash to display in detail about the transaction.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |

### Example Request and Response


```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/tx/data/arweave?hash=3NDXWouOXjWCVAkdIbjXTw91SNVRljwHiMoR3IavEac&network=mainnet' \
--header 'X-API-KEY: ******************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "******************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/tx/data/arweave?hash=3NDXWouOXjWCVAkdIbjXTw91SNVRljwHiMoR3IavEac&network=mainnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "transaction_hash": "3NDXWouOXjWCVAkdIbjXTw91SNVRljwHiMoR3IavEac",
  "from": "1BmeoGRnPXOv2eyl5CnccIPBrD0axEPQBal3NuSJCvI",
  "to": "MBB9dcPWUG_t75ezcBwt7u3C0vCyu4tuwxjstlCpvIE",
  "value": 12734.9,
  "gas_price": "0.000000862848",
  "signature": "K61Z7EDckRRyxY_dRRd3cy_6P72fwCEkifl1QQp9cOxXmhSSMKJcIESwYM_6jFT-XEMVGqDWXTrG6sKRp4KhvietgTV0Bk09GSMMjtDZb7SFqW-uDo6ivL4UjV_9fFYqzWuD7QU5NQbZvNXHm-Lea6tQ6_Rod2nLMiBsazWoy7kV6JSQVP1hZeIcAthc4wPgUcolTqo7zQ2a9xV0V8ClsmaqzNorUaztdUghAKBXJWmipwO-W0xhWnQlXFmE_QvikO8OI2b3YvsaOMaVdMdtI4cvUlcXmYW0xZXbQ6sTt4K3b9mXUWg5CNWasBi_d_zGY8jo6uczn6JJsqjA5dc5rtIZdJk3iBOEKm_WTyHAC2Q8Zac6CVKwjOW9zZ63znqEX0RHbUHdT9TtFme14NaYjLH6oS_KT2mi3BoCy39JBcCiprmbsWjlaqVicoJKdhPebS4KlXx3PLyxPP9EfbhopQ3YO55lI6tVp37R4LvHnekgmebjpwAK7g-N_RTG3HX_qCAltaayVMdVpn0zaYo_rYSTcfNhlN5emAF4PyeyLaOEc-5dXUQoidKE29T-ijRPr95cDEX205rmd8tpHsWq1bDyqlVsyvWKgHjffj8KbPAWUvEfONj3GD2IsaHEvYn6KFPQ5UV-WN4lxOWWHnnEhHZxXzirDjhFjkC2dJ3MjRQ"
}
```


```mdx-code-block
</TabItem>

</Tabs>
```

### GET Bitcoin

```

https://faas-test.dojima.network/dojima-faas/v1/tx/data/bitcoin?hash=40a9606c5b8a3375a345f110ac81685848f75ab4bd1896ce90383826eeecdd84&network=testnet
```

**Returns transaction details by hash for bitcoin.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**hash**   |  **Required.** Transaction hash to display in detail about the transaction.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |

### Example Request and Response


```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/tx/data/bitcoin?hash=40a9606c5b8a3375a345f110ac81685848f75ab4bd1896ce90383826eeecdd84&network=testnet' \
--header 'X-API-KEY: *******************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "*******************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/tx/data/bitcoin?hash=40a9606c5b8a3375a345f110ac81685848f75ab4bd1896ce90383826eeecdd84&network=testnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "txid": "40a9606c5b8a3375a345f110ac81685848f75ab4bd1896ce90383826eeecdd84",
  "size": 245,
  "version": 2,
  "locktime": 0,
  "fee": 0.00028386,
  "inputs": [
    {
      "coinbase": false,
      "txid": "a10a458b4816dd38d5104db5b493519801faa56bfcb30cbcfc0afbe7f1851397",
      "output": 2,
      "sigscript": "",
      "sequence": 4294967295,
      "pkscript": "00143b8b9de28b699d8f3621bf0383fd617b65b84f0a",
      "value": 61755,
      "address": "tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp",
      "witness": [
        "3044022030820c9664c5244a1e285aa1c77f485e7dfad9ff656ac05ec5cc98203c52d46602201eddb2f9f063f4611656dcee1c203fda42933dc7e6eb970355867da1c43f4a1701",
        "025cfbe662e8c3e660094116f94d3020f30787c8252a62b32088464e65cf700e8c"
      ]
    }
  ],
  "outputs": [
    {
      "address": "tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp",
      "pkscript": "00143b8b9de28b699d8f3621bf0383fd617b65b84f0a",
      "value": 317,
      "spent": false,
      "spender": null
    },
    {
      "address": null,
      "pkscript": "6a0c535741503a4254432e425443",
      "value": 0,
      "spent": false,
      "spender": null
    },
    {
      "address": "tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp",
      "pkscript": "00143b8b9de28b699d8f3621bf0383fd617b65b84f0a",
      "value": 33052,
      "spent": false,
      "spender": null
    }
  ],
  "block": {
    "height": 2252852,
    "position": 3
  },
  "deleted": false,
  "timestamp": "Tue, 31 May 2022 14:49:29 GMT",
  "rbf": false,
  "weight": 653,
  "from": "tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp",
  "fromValue": 0.00061755,
  "to1": "tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp",
  "to1Value": 0.00000317,
  "to2": null,
  "to2Value": 0
}
```


```mdx-code-block
</TabItem>

</Tabs>
```

### GET Solana

```

https://faas-test.dojima.network/dojima-faas/v1/tx/data/solana?hash=34RSHscH1t8vgfBjmrtaSbWwMb514ACX9wgXniq6FkjYU9dvqnYJxrMuhnbJWYpekQt1NJpHPo2yroFFmqTMUkFX&network=devne
```

**Returns transaction details by hash for solana.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

!!! note
    Note: Never share, disclouse or save 'apikey' publicly.


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params



|  Parameter|     Description              |
|-----------|--------------------------------------|
|**hash**   |  **Required.** Transaction hash to display in detail about the transaction.|
| **network**   |**Required:** Default 'mainnet'. Arweave doesn't have 'testnet' explorer to display transactions. |
| **state**   | Optional. Default 'confirmed'. Either 'confirmed' or 'finality'' |

### Example Request and Response


```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```
**cURL**
```
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/tx/data/solana?hash=2dQaVetThxgW4v3qn2aPVa5cNQ21HgeMYHrSq7G2sxS4rFn25f9PpjjvUBdVzJdqWYbsMV7AY6x8M653DJeGdPuu&network=devnet' \
--header 'X-API-KEY: **********************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "**********************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/tx/data/solana?hash=2dQaVetThxgW4v3qn2aPVa5cNQ21HgeMYHrSq7G2sxS4rFn25f9PpjjvUBdVzJdqWYbsMV7AY6x8M653DJeGdPuu&network=devnet", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
{
  "timeStamp": 1654094563,
  "gasFee": 0.000005,
  "amount": 0.01,
  "status": "",
  "block": 138189622,
  "from": "DxehLnrWp8iP5ahoG413BD4azVrkgA8Pob4rXco3mpCS",
  "to": "71RGPwytVSNgT9i5RJhwvt7mMSahqxEYFat43ijZ8hbU",
  "recentBlockHash": "4dYWo3CgRGvjjxXgrgFo8wVYXRZuS8UCam5Ps7NM4BKg",
  "instructionData": "3Bxs4NN8M2Yn4TLb"
}
```
```mdx-code-block
</TabItem>

</Tabs>
```




