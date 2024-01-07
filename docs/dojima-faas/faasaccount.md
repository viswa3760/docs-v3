---
title :  Account
---

**These endpoints return details such as public address from seed phrase/mnemonic, balance of the respective input token.**

### GET Address

```

 https://faas-test.dojima.network/dojima-faas/v1/account/address?mnemonic=letter ethics correct bus asset pipe tourist vapor envelope kangaroo warm dawn&network=testnet

```

**Returns public addresses of the provided seed phrase of the user and network type.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   | c226c9df7eb08c82c4f4c22266dd <br/> **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Public address of the respective tokens were generated:

    - Bitcoin
    - Arweave
    - Ethereum
    - Solana 


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**mnemonic**   | letter ethics correct bus asset pipe tourist vapor envelope kangaroo warm dawn<br/> **Required:** Seed phrase of the user to generate addresses.|
| **network**   | testnet <br/>**Required:** 'mainnet or testnet or devnet'

### Example Request and Response


=== "REQUEST"
    **cURL.**
    ```

    curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/account/address?mnemonic=******************************************************&network=testnet' \
    --header 'X-API-KEY: ********************'

    ```

    **Java Script.**

    ``` javascript
    var myHeaders = new Headers();
    myHeaders.append("X-API-KEY", "********************");

    var requestOptions = {
      method: 'GET',
      headers: myHeaders,
      redirect: 'follow'
    };

    fetch("https://faas-test.dojima.network/dojima-faas/v1/account/address?mnemonic=******************************************************&network=testnet", requestOptions)
      .then(response => response.text())
      .then(result => console.log(result))
      .catch(error => console.log('error', error));
    ```

=== "Response"
    
     ``` json
      {
        "arweave": "7zzxJgYHgDlaURc3xt3wvLITPp6I8oIpYj_yg_xirb4",
        "bitcoin": "tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp",
        "ethereum": "0x0577e1E35C4f30cA8379269B7Fd85cBCE7F084f4",
        "solana": "DxehLnrWp8iP5ahoG413BD4azVrkgA8Pob4rXco3mpCS"
      }
     ```


### GET Token Balance

```
https://faas-test.dojima.network/dojima-faas/v1/account/balance?address=tb1q8w9emc5tdxwc7d3phupc8ltp0djmsnc2ngxnpp&asset=bitcoin&network=testnet
```
**Returns balance of the token based on inputs.**

### HEADERS

>  Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.

|  Parameter|     Description              |
|-----------|--------------------------------------|
|**X-API-KEY**   | c226c9df7eb08c82c4f4c22266dd <br/> **Required**: Api Key of the user for endpoint to generate result |


### Params

!!! note
    Public address of the respective tokens were generated:
    
    - Bitcoin
    - Arweave
    - Ethereum
    - Solana 


|  Parameter|     Description              |
|-----------|--------------------------------------|
|**mnemonic**   | letter ethics correct bus asset pipe tourist vapor envelope kangaroo warm dawn<br/> **Required:** Seed phrase of the user to generate addresses.|
| **network**   | testnet <br/>**Required:** 'mainnet or testnet or devnet'

## Example Request and Response


=== "REQUEST"
    **cURL.**
    ```

    curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/account/address?mnemonic=******************************************************&network=testnet' \
    --header 'X-API-KEY: ********************'

    ```

    **Java Script.**

    ``` javascript
    var myHeaders = new Headers();
    myHeaders.append("X-API-KEY", "********************");

    var requestOptions = {
      method: 'GET',
      headers: myHeaders,
      redirect: 'follow'
    };

    fetch("https://faas-test.dojima.network/dojima-faas/v1/account/address?mnemonic=******************************************************&network=testnet", requestOptions)
      .then(response => response.text())
      .then(result => console.log(result))
      .catch(error => console.log('error', error));
    ```
=== "Response"
    
     ``` json
      {
        "key": "6",
        "name": "robot",
        "email":  "robot@gmail.com",
        "apiKey": "**********************",
        "plan":"monthly",
        "limit":"100000",
        "createdAt": "2022-08-04T05:02:19.000Z",
        "validUntil": "2022-09-03T05:02:19.623Z",
        "updatedAt": "2022-08-04T05:02:19.000Z"
      }
     ```
      
