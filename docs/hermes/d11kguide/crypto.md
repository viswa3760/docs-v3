---
title: Crypto
---

# `@d11k-ts/crypto`

The D11K CRYPTO package is a crypto package used by all `D11K` clients.

D11K-CRYPTO encrypts a master phrase to a keystore. This keystore can then be exported to other D11K wallets or stored securely.

Users can export their phrase and import them into other wallets since it is a BIP39 compatible phrase.

## Installation

- Install `@d11k-ts/crypto` from `npm`

```bash
yarn add @d11k-ts/crypto
```

## Build

```bash
yarn build
```

## Tests

```bash
yarn test
```

### Constants

```js
// Crypto Constants for chain
const cipher = 'aes-128-ctr'
const kdf = 'pbkdf2'
const prf = 'hmac-sha256'
const dklen = 32
const c = 262144
const hashFunction = 'sha256'
const meta = 'd11k-keystore'
```

#### Keystore Type

```ts
export type Keystore = {
  address: string,
  crypto: {
    cipher: string,
    ciphertext: string,
    cipherparams: {
      iv: string
    },
    kdf: string,
    kdfparams: {
      prf: string,
      dklen: number,
      salt: string,
      c: number,
    },
    mac: string,
  },
  id: string,
  version: number,
  meta: string,
}
```
