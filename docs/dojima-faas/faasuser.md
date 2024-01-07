---
title :  User
---

**These endpoints are used to create, delete, find or update user.**

## POST Create user

```

 https://faas-test.dojima.network/dojima-faas/v1/user/create?name=robot1&email=robot1@gmail.com&plan=monthly

```



**Returns user details along with apikey based on inputs provided.**

## PARAMS

|           |                                      |
|-----------|--------------------------------------|
|**name**   |robot1 <br/>Required. Name of the user|
|**email**  |`robot1@gmail.com` <br/> Required. Provide valid email of the user to receive updates or notifications |
| **plan**  | monthly<br/>  Required. 'monthly or yearly'. Provide a plan type to get access until the selected period. <br/> > monthly - 10,000 calls/month yearly - 1,80,000 calls/year |

## Example Request and Response

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
curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/user/data?api=*******************'

```

**Java Script**

```js
var requestOptions = {
  method: 'POST',
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/user/create?name=robot&email=robot@gmail.com&plan=monthly", requestOptions)
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
  "key": 6,
  "name": "robot",
  "email": "robot@gmail.com",
  "apiKey": "**********************",
  "plan": "monthly",
  "limit": 100000,
  "createdAt": "2022-08-04T05:02:19.000Z",
  "validUntil": "2022-09-03T05:02:19.623Z",
  "updatedAt": "2022-08-04T05:02:19.000Z"
}

```


```mdx-code-block
</TabItem>

</Tabs>
```

## GET Find user

```

https://faas-test.dojima.network/dojima-faas/v1/user/data?api=c226c9df7eb08c82c4f4c22266dd

```
Query Parameters

|Parameters | Description                          |
|-----------|--------------------------------------|
|**api**    |c226c9df7eb08c82c4f4c22266dd          |

## Example Request and Response


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

curl --location --request GET 'https://faas-test.dojima.network/dojima-faas/v1/user/data?api=*******************'

```

**Java Script**

```js
var myHeaders = new Headers();
myHeaders.append("X-API-KEY", "****************");

var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("https://faas-test.dojima.network/dojima-faas/v1/user/data?api=*******************", requestOptions)
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
  "key": 6,
  "name": "robot",
  "email": "robot@gmail.com",
  "apiKey": "**********************",
  "plan": "monthly",
  "limit": 100000,
  "createdAt": "2022-08-04T05:02:19.000Z",
  "validUntil": "2022-09-03T05:02:19.623Z",
  "updatedAt": "2022-08-04T05:02:19.000Z"
}

```


```mdx-code-block
</TabItem>

</Tabs>
```