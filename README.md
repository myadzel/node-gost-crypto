node-gost-crypto
================

About
-------

Node.js implementation of WebCrypto API interfaces and Public Key Infrastructure for GOST algorithms (Russian Cryptographic Standards)

Based on library WebCrypto GOST https://github.com/rudonick/crypto

Usage example
-------

Install
>$ npm install node-gost-crypto


Usage in Node.js

```js
const { gostCrypto, gostEngine } = require('node-gost-crypto');

const str = 'тест';

// $ echo -en '\xD1\x82\xD0\xB5\xD1\x81\xD1\x82' | openssl dgst -md_gost94
// 048fcd8d361b7a039bdc3b1906d8128fd3bfd968047ea2b7e930159357388269

const buffer = Buffer.from(str);

// using engine
const digest = gostEngine.getGostDigest({name: 'GOST R 34.11', length: 256, version: 1994});
console.log(Buffer.from(digest.digest(buffer)).toString('hex'));

// using crypto
gostCrypto.subtle.digest('GOST R 34.11-94-256', buffer).then((arrayBuffer) => {
    console.log(Buffer.from(arrayBuffer).toString('hex'));
});
```

License
-------

MIT
