---
title: Prices Stats
---
**These endpoints return details such as token latest prices, stats, history based particular date or past n days or in between certain dates.**

### GET Token latest price

```

https://faas-test.dojima.network/dojima-faas/v1/prices/latest/token?tokenName=solana

```

**Returns token current price, market_cap, volume, supply, data related to ath (all time high), atl (all time low).**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

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
|**mnemonic**   |  **Required:** Seed phrase of the user to generate addresses.|
| **network**   |**Required:** 'mainnet or testnet or devnet' |

### Example Request and Response



=== "REQUEST"
    **cURL**
    ```
    curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/prices/latest/token?tokenName=solana' \
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

    fetch("https://faas-test.dojima.network/dojima-faas/v1/prices/latest/token?tokenName=solana", requestOptions)
      .then(response => response.text())
      .then(result => console.log(result))
      .catch(error => console.log('error', error));
    ```
=== "Response"
    
     ``` json
      {
        "current_price": 39.19,
        "market_cap": 13566176494,
        "total_volume": 1491902699,
        "circulating_supply": 346652190.616162,
        "total_supply": 508180963.57,
        "max_supply": null,
        "ath": 259.96,
        "ath_change_percentage": -84.96585,
        "ath_date": "Sat, 06 Nov 2021 21:54:35 GMT",
        "atl": 0.500801,
        "atl_change_percentage": 7704.02799,
        "atl_date": "Mon, 11 May 2020 19:35:23 GMT"
      }
     ```

### GET Token latest stats

```
https://faas-test.dojima.network/dojima-faas/v1/prices/latest/stats?token=BTC
```
**Returns token stats related to addresses, blocks, transactions, supply, etc.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   | **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Token list:

    - btc
    - ar
    - eth
    - sol

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**token**   | **Required**: Token id to retrieve stats related to addresses, blocks, transactions, supply, etc.|

## Example Request and Response


=== "REQUEST"
  **cURL Commands**
```

curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/prices/latest/stats?token=BTC' \
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

fetch("https://faas-test.dojima.network/dojima-faas/v1/prices/latest/stats?token=BTC", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));

```
=== "Response"
    
     ``` json
      {
        "current_price": 39.19,
        "market_cap": 13566176494,
        "total_volume": 1491902699,
        "circulating_supply": 346652190.616162,
        "total_supply": 508180963.57,
        "max_supply": null,
        "ath": 259.96,
        "ath_change_percentage": -84.96585,
        "ath_date": "Sat, 06 Nov 2021 21:54:35 GMT",
        "atl": 0.500801,
        "atl_change_percentage": 7704.02799,
        "atl_date": "Mon, 11 May 2020 19:35:23 GMT"
      }
     ```

```mdx-code-block
<Tabs
    defaultValue="request"
    values={[
        {label: 'REQUEST', value: 'request'},
         {label: 'RESPONSE', value: 'response'},
          
    ]}>
<TabItem value="request">
```

**cURL Commands**
```

curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/prices/latest/stats?token=BTC' \
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

fetch("https://faas-test.dojima.network/dojima-faas/v1/prices/latest/stats?token=BTC", requestOptions)
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
  "id": 1182,
  "time": 1659484800,
  "symbol": "BTC",
  "partner_symbol": "BTC",
  "zero_balance_addresses_all_time": 985144574,
  "unique_addresses_all_time": 1027159686,
  "new_addresses": 417758,
  "active_addresses": 979238,
  "average_transaction_value": 15.41044161368356,
  "block_height": 747864,
  "hashrate": 199187870.17167962,
  "difficulty": 27692567959233.59,
  "block_time": 597.1180555555553,
  "block_size": 1292170,
  "current_supply": 19111662,
  "transaction_count": 282037,
  "transaction_count_all_time": 753969557,
  "large_transaction_count": 18486
}

```


```mdx-code-block
</TabItem>

</Tabs>
```

### GET History by date

```
https://faas-test.dojima.network/dojima-faas/v1/prices/history/date?tokenName=bitcoin&date=05-07-2021
```
**Returns token price, market_cap and total_volume on a particular date.**


### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Token list:


    - bitcoin
    - arweave
    - ethereum
    - solana
    - usd-coin


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**tokenName**   | **Required:** token price, market_cap and total_volume on a particular date.|
| **days**   |**Required.** DD-MM-YYYY format date |

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
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/prices/history/date?tokenName=bitcoin&date=22-05-2022' \
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

fetch("https://faas-test.dojima.network/dojima-faas/v1/prices/history/date?tokenName=bitcoin&date=22-05-2022", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
[
  {
    "current_price": 29491.507947760598,
    "market_cap": 561696351558.8424,
    "total_volume": 13561006428.368963
  }
]

```


```mdx-code-block
</TabItem>

</Tabs>
```

### GET GET History by days

```
https://faas-test.dojima.network/dojima-faas/v1/prices/history/days?tokenName=bitcoin&days=20
```
**Returns token prices, market_cap and total_volume for mentioned no. of days. Minutely data for 1 day, hourly data for 1.**


### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Token list:
    
    - bitcoin
    - arweave
    - ethereum
    - solana
    - usd-coin


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**tokenName**   | **Required:** token price, market_cap and total_volume on a particular date.|
| **date**   |**Required.** Token prices, market_cap and total_volume for mentioned no. of days. Minutely data for 1 day, hourly data for 1<days<=10 and daily data for 10 < days |

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
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/prices/history/days?tokenName=bitcoin&days=20' \
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

fetch("https://faas-test.dojima.network/dojima-faas/v1/prices/history/days?tokenName=bitcoin&days=20", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));

```

```mdx-code-block
</TabItem>
<TabItem value="response">
```


```json
[
  {
    "prices": [
      {
        "date": "Sat, 16 Jul 2022 00:00:00 GMT",
        "price": 20794.811981436706
      },
      {
        "date": "Sun, 17 Jul 2022 00:00:00 GMT",
        "price": 21193.08334336837
      },
      {
        "date": "Mon, 18 Jul 2022 00:00:00 GMT",
        "price": 20824.36275165164
      },
      {
        "date": "Tue, 19 Jul 2022 00:00:00 GMT",
        "price": 22395.365383103952
      },
      {
        "date": "Wed, 20 Jul 2022 00:00:00 GMT",
        "price": 23366.90769792785
      },
      {
        "date": "Thu, 21 Jul 2022 00:00:00 GMT",
        "price": 23313.296731959555
      },
      {
        "date": "Fri, 22 Jul 2022 00:00:00 GMT",
        "price": 23155.207555248304
      },
      {
        "date": "Sat, 23 Jul 2022 00:00:00 GMT",
        "price": 22696.902754290055
      },
      {
        "date": "Sun, 24 Jul 2022 00:00:00 GMT",
        "price": 22506.199573628986
      },
      {
        "date": "Mon, 25 Jul 2022 00:00:00 GMT",
        "price": 22613.719208248454
      },
      {
        "date": "Tue, 26 Jul 2022 00:00:00 GMT",
        "price": 21330.295450788173
      },
      {
        "date": "Wed, 27 Jul 2022 00:00:00 GMT",
        "price": 21235.612316085775
      },
      {
        "date": "Thu, 28 Jul 2022 00:00:00 GMT",
        "price": 22908.884260468687
      },
      {
        "date": "Fri, 29 Jul 2022 00:00:00 GMT",
        "price": 23822.067597823116
      },
      {
        "date": "Sat, 30 Jul 2022 00:00:00 GMT",
        "price": 23847.58331873861
      },
      {
        "date": "Sun, 31 Jul 2022 00:00:00 GMT",
        "price": 23653.459549430798
      },
      {
        "date": "Mon, 01 Aug 2022 00:00:00 GMT",
        "price": 23379.70052509082
      },
      {
        "date": "Tue, 02 Aug 2022 00:00:00 GMT",
        "price": 23333.749243312184
      },
      {
        "date": "Wed, 03 Aug 2022 00:00:00 GMT",
        "price": 23053.846847482677
      },
      {
        "date": "Thu, 04 Aug 2022 00:00:00 GMT",
        "price": 22860.42098438317
      },
      {
        "date": "Thu, 04 Aug 2022 10:25:46 GMT",
        "price": 22950.523475823156
      }
    ],
    "market_cap": [
      {
        "date": "Sat, 16 Jul 2022 00:00:00 GMT",
        "price": 397285233065.65533
      },
      {
        "date": "Sun, 17 Jul 2022 00:00:00 GMT",
        "price": 404705642580.89075
      },
      {
        "date": "Mon, 18 Jul 2022 00:00:00 GMT",
        "price": 397660610560.5498
      },
      {
        "date": "Tue, 19 Jul 2022 00:00:00 GMT",
        "price": 425756736660.6174
      },
      {
        "date": "Wed, 20 Jul 2022 00:00:00 GMT",
        "price": 445889013251.1064
      },
      {
        "date": "Thu, 21 Jul 2022 00:00:00 GMT",
        "price": 446130012149.91077
      },
      {
        "date": "Fri, 22 Jul 2022 00:00:00 GMT",
        "price": 442379611364.02734
      },
      {
        "date": "Sat, 23 Jul 2022 00:00:00 GMT",
        "price": 433485926857.3929
      },
      {
        "date": "Sun, 24 Jul 2022 00:00:00 GMT",
        "price": 429803379587.55133
      },
      {
        "date": "Mon, 25 Jul 2022 00:00:00 GMT",
        "price": 433819662321.5266
      },
      {
        "date": "Tue, 26 Jul 2022 00:00:00 GMT",
        "price": 407480099599.8142
      },
      {
        "date": "Wed, 27 Jul 2022 00:00:00 GMT",
        "price": 405692421501.52716
      },
      {
        "date": "Thu, 28 Jul 2022 00:00:00 GMT",
        "price": 437193517021.8447
      },
      {
        "date": "Fri, 29 Jul 2022 00:00:00 GMT",
        "price": 454806622614.75885
      },
      {
        "date": "Sat, 30 Jul 2022 00:00:00 GMT",
        "price": 459609388579.5554
      },
      {
        "date": "Sun, 31 Jul 2022 00:00:00 GMT",
        "price": 451726702392.36206
      },
      {
        "date": "Mon, 01 Aug 2022 00:00:00 GMT",
        "price": 447051019373.1847
      },
      {
        "date": "Tue, 02 Aug 2022 00:00:00 GMT",
        "price": 445958949620.3002
      },
      {
        "date": "Wed, 03 Aug 2022 00:00:00 GMT",
        "price": 440954684720.7478
      },
      {
        "date": "Thu, 04 Aug 2022 00:00:00 GMT",
        "price": 437035641450.2815
      },
      {
        "date": "Thu, 04 Aug 2022 10:25:46 GMT",
        "price": 438396573850.57587
      }
    ],
    "total_volume": [
      {
        "date": "Sat, 16 Jul 2022 00:00:00 GMT",
        "price": 46542248374.33238
      },
      {
        "date": "Sun, 17 Jul 2022 00:00:00 GMT",
        "price": 42051101694.797554
      },
      {
        "date": "Mon, 18 Jul 2022 00:00:00 GMT",
        "price": 29615794461.49923
      },
      {
        "date": "Tue, 19 Jul 2022 00:00:00 GMT",
        "price": 58636734705.48306
      },
      {
        "date": "Wed, 20 Jul 2022 00:00:00 GMT",
        "price": 57338223361.51413
      },
      {
        "date": "Thu, 21 Jul 2022 00:00:00 GMT",
        "price": 40775718993.79776
      },
      {
        "date": "Fri, 22 Jul 2022 00:00:00 GMT",
        "price": 63224249257.511284
      },
      {
        "date": "Sat, 23 Jul 2022 00:00:00 GMT",
        "price": 40304373301.41499
      },
      {
        "date": "Sun, 24 Jul 2022 00:00:00 GMT",
        "price": 42519262113.1533
      },
      {
        "date": "Mon, 25 Jul 2022 00:00:00 GMT",
        "price": 33108916659.05373
      },
      {
        "date": "Tue, 26 Jul 2022 00:00:00 GMT",
        "price": 42667548128.932236
      },
      {
        "date": "Wed, 27 Jul 2022 00:00:00 GMT",
        "price": 53995620035.18145
      },
      {
        "date": "Thu, 28 Jul 2022 00:00:00 GMT",
        "price": 54498281944.45157
      },
      {
        "date": "Fri, 29 Jul 2022 00:00:00 GMT",
        "price": 55609627980.6571
      },
      {
        "date": "Sat, 30 Jul 2022 00:00:00 GMT",
        "price": 41089335195.63975
      },
      {
        "date": "Sun, 31 Jul 2022 00:00:00 GMT",
        "price": 62102072346.807785
      },
      {
        "date": "Mon, 01 Aug 2022 00:00:00 GMT",
        "price": 31786729326.443203
      },
      {
        "date": "Tue, 02 Aug 2022 00:00:00 GMT",
        "price": 44489771146.510735
      },
      {
        "date": "Wed, 03 Aug 2022 00:00:00 GMT",
        "price": 35151096516.75639
      },
      {
        "date": "Thu, 04 Aug 2022 00:00:00 GMT",
        "price": 41334593234.075066
      },
      {
        "date": "Thu, 04 Aug 2022 10:25:46 GMT",
        "price": 23908600834.73234
      }
    ]
  }
]

```


```mdx-code-block
</TabItem>

</Tabs>
```
### GET History by date range

```
https://faas-test.dojima.network/dojima-faas/v1/prices/history/date?tokenName=bitcoin&date=05-07-2021
```
**Returns token price, market_cap and total_volume for date range. 5 minute interval data data if date difference 1 day, hourly data if date difference is between 1 and 90 and daily data if date difference is more than 90.**


### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   |  **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Token list:

    - bitcoin
    - arweave
    - ethereum
    - solana
    - usd-coin


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**tokenName**   | **Required:** token price, market_cap and total_volume on a particular date.|
| **fromDate**   | **Required:** YYYY-MM-DD format date |
| **thruDate**   | **Required.** YYYY-MM-DD format date    |

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
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/prices/history/date/range?tokenName=bitcoin&fromDate=2022-05-01&thruDate=2022-05-11' \
--header 'X-API-KEY: *****************'
```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "*****************");

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/prices/history/date/range?tokenName=bitcoin&fromDate=2022-05-01&thruDate=2022-05-31", requestOptions)
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
  "prices": [
    {
      "date": "Sat, 16 Jul 2022 00:00:00 GMT",
      "price": 1234.0991389763224
    },
    {
      "date": "Sun, 17 Jul 2022 00:00:00 GMT",
      "price": 1355.04564021949
    },
    {
      "date": "Mon, 18 Jul 2022 00:00:00 GMT",
      "price": 1344.7202840019017
    },
    {
      "date": "Tue, 19 Jul 2022 00:00:00 GMT",
      "price": 1570.6589588642053
    },
    {
      "date": "Wed, 20 Jul 2022 00:00:00 GMT",
      "price": 1542.6298214332235
    },
    {
      "date": "Thu, 21 Jul 2022 00:00:00 GMT",
      "price": 1527.4139307593093
    },
    {
      "date": "Fri, 22 Jul 2022 00:00:00 GMT",
      "price": 1576.8252394976823
    },
    {
      "date": "Sat, 23 Jul 2022 00:00:00 GMT",
      "price": 1536.124922238913
    },
    {
      "date": "Sun, 24 Jul 2022 00:00:00 GMT",
      "price": 1552.4964891908746
    },
    {
      "date": "Mon, 25 Jul 2022 00:00:00 GMT",
      "price": 1601.2079670127046
    },
    {
      "date": "Tue, 26 Jul 2022 00:00:00 GMT",
      "price": 1450.4822852139405
    },
    {
      "date": "Tue, 26 Jul 2022 04:59:49 GMT",
      "price": 1431.2771658285428
    }
  ],
  "market_cap": [
    {
      "date": "Sat, 16 Jul 2022 00:00:00 GMT",
      "price": 147677565536.3019
    },
    {
      "date": "Sun, 17 Jul 2022 00:00:00 GMT",
      "price": 161839496479.48514
    },
    {
      "date": "Mon, 18 Jul 2022 00:00:00 GMT",
      "price": 161551223982.244
    },
    {
      "date": "Tue, 19 Jul 2022 00:00:00 GMT",
      "price": 187518878564.43118
    },
    {
      "date": "Wed, 20 Jul 2022 00:00:00 GMT",
      "price": 184299116474.0005
    },
    {
      "date": "Thu, 21 Jul 2022 00:00:00 GMT",
      "price": 183383314168.63928
    },
    {
      "date": "Fri, 22 Jul 2022 00:00:00 GMT",
      "price": 188807814065.77225
    },
    {
      "date": "Sat, 23 Jul 2022 00:00:00 GMT",
      "price": 183933879174.97644
    },
    {
      "date": "Sun, 24 Jul 2022 00:00:00 GMT",
      "price": 185766674503.14
    },
    {
      "date": "Mon, 25 Jul 2022 00:00:00 GMT",
      "price": 192833875418.8718
    },
    {
      "date": "Tue, 26 Jul 2022 00:00:00 GMT",
      "price": 176371406952.78534
    },
    {
      "date": "Tue, 26 Jul 2022 04:59:49 GMT",
      "price": 171509003635.7274
    }
  ],
  "total_volume": [
    {
      "date": "Sat, 16 Jul 2022 00:00:00 GMT",
      "price": 16817194904.2499
    },
    {
      "date": "Sun, 17 Jul 2022 00:00:00 GMT",
      "price": 19025831554.91271
    },
    {
      "date": "Mon, 18 Jul 2022 00:00:00 GMT",
      "price": 15797648344.457474
    },
    {
      "date": "Tue, 19 Jul 2022 00:00:00 GMT",
      "price": 26437290054.27533
    },
    {
      "date": "Wed, 20 Jul 2022 00:00:00 GMT",
      "price": 27749085857.707005
    },
    {
      "date": "Thu, 21 Jul 2022 00:00:00 GMT",
      "price": 21728126383.56131
    },
    {
      "date": "Fri, 22 Jul 2022 00:00:00 GMT",
      "price": 19411405082.967407
    },
    {
      "date": "Sat, 23 Jul 2022 00:00:00 GMT",
      "price": 18084368731.242767
    },
    {
      "date": "Sun, 24 Jul 2022 00:00:00 GMT",
      "price": 14901008279.154797
    },
    {
      "date": "Mon, 25 Jul 2022 00:00:00 GMT",
      "price": 16058331978.02615
    },
    {
      "date": "Tue, 26 Jul 2022 00:00:00 GMT",
      "price": 19852493229.276333
    },
    {
      "date": "Tue, 26 Jul 2022 04:59:49 GMT",
      "price": 19607955073.403877
    }
  ]
}

```

```mdx-code-block
</TabItem>

</Tabs>
```