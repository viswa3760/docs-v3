---
id: dojimafaas
title: Dojima-FaaS
---

## Dojima faas


Dojima faas provides you blockchain functionality as a service. Blockchain functionality such as creating an account, gas rates for transaction, signing transaction, dollar price, transaction history, submit transaction e.t.c.

## Features

- **One Api** - Single endpoint for all blockchain functionality to develop dapps.
- **Create Account** - create an account for any blockchain by just providing a chain name.
- **Gas Rates** - slow, average, fast gas rates for transaction to be processed.
- **Dollar price** - dollar price of any token instantly.
- **Transaction history** - transaction history of any blockchain providing necessary details.
- **Price History** - price of daily, weekly, yearly, all-time token.

## User

**These endpoints are used to create, delete, find or update user.**



POST **Create user**

```
 https://faas-test.dojima.network/dojima-faas/v1/user/create?name=robot1&email=robot1@gmail.com&plan=monthly

```



**Returns user details along with apikey based on inputs provided.**



### PARAMS

|           |                                      |
|-----------|--------------------------------------|
|**name**   |robot1 <br/>Required. Name of the user|
|**email**  |`robot1@gmail.com` <br/> Required. Provide valid email of the user to receive updates or notifications |
| **plan**  | monthly<br/>  Required. 'monthly or yearly'. Provide a plan type to get access until the selected period. <br/> > monthly - 10,000 calls/month yearly - 1,80,000 calls/year |

GET **Find user**



```
 https://faas-test.dojima.network/dojima-faas/v1/user/data?api=c226c9df7eb08c82c4f4c22266dd

```

|           |                                      |
|-----------|--------------------------------------|
|**api**    |c226c9df7eb08c82c4f4c22266dd          |

## Account
**These endpoints return details such as public address from seed phrase/mnemonic, balance of the respective input token.**

GET **Address**

```
 https://faas-test.dojima.network/dojima-faas/v1/account/address?mnemonic=letter ethics correct bus asset pipe tourist vapor envelope kangaroo warm dawn&network=testnet
```

**Returns public addresses of the provided seed phrase of the user and network type.**

### HEADERS

|           |                                      |
|-----------|--------------------------------------|
|**X-API-KEY**    |c226c9df7eb08c82c4f4c22266dd <br/> Required. Api Key of the user for endpoint to generate result<br/> Doesn't have one? Navigate to "User->Create user" endpoint and get one. <br/>Note: Never share, disclouse or save 'apikey' publicly.         |


