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

const stringToArrayBuffer = (str) => {
    const array = new Uint8Array(str.length);
    for (let i = 0; i < str.length; i++) {
        array[i] = str.charCodeAt(i);
    }
    return array.buffer;
};

const arrayBufferToHexString = (buffer) => {
    return Array.prototype.map.call(new Uint8Array(buffer), (data) => {
        return ('00' + data.toString(16)).slice(-2);
    }).join('');
};

const str = '';

// $ | openssl dgst -md_gost94
// 981e5f3ca30c841487830f84fb433e13ac1101569b9c13584ac483234cd656c0

// using engine
const digest = gostEngine.getGostDigest({name: 'GOST R 34.11', length: 256, version: 1994});
console.log(arrayBufferToHexString(digest.digest(stringToArrayBuffer(str))));

// using crypto
gostCrypto.subtle.digest('GOST R 34.11-94-256', stringToArrayBuffer(str)).then((buf) => {
    console.log(arrayBufferToHexString(buf));
});
```

License
-------

MIT
