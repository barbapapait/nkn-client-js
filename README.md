[![CircleCI Status](https://circleci.com/gh/nknorg/nkn-client-js.svg?style=shield&circle-token=:circle-token)](https://circleci.com/gh/nknorg/nkn-client-js)

# nkn-client-js

JavaScript implementation of NKN client.

Send and receive data between any NKN clients without setting up a server.

Note: This is a **client** version of the NKN protocol, which can send and
receive data but **not** relay data (mining). For **node** implementation which
can mine NKN token by relaying data, please refer to
[nkn](https://github.com/nknorg/nkn/).

**Note: This repository is in the early development stage and may not have all
functions working properly. It should be used only for testing now.**

## Usage

For npm:

```shell
npm install nkn-client
```

And then in your code:

```javascript
const nkn = require('nkn-client');
```

For browser, use `dist/nkn.js` or `dist/nkn.min.js`.

Create a client with a generated key pair:

```javascript
const client = nkn();
```

Or with an identifier (used to distinguish different clients sharing the same
key pair):

```javascript
const client = nkn({
  identifier: 'any string',
});
```

Get client key pair:

```javascript
console.log(client.key.privateKey, client.key.publicKey);
```

Create a client using an existing private key:

```javascript
const client = nkn({
  identifier: 'any string',
  privateKey: 'cd5fa29ed5b0e951f3d1bce5997458706186320f1dd89156a73d54ed752a7f37',
});
```

By default the client will use bootstrap RPC server (for getting node address)
provided by us. Any NKN full node can serve as a bootstrap RPC server. To create
a client using customized bootstrap RPC server:

```javascript
const client = nkn({
  identifier: 'any string',
  seedRpcServerAddr: 'https://xxx',
});
```

Private key should be kept **SECRET**! Never put it in version control system
like here.

Get client identifier:

```javascript
console.log(client.identifier);
```

And client NKN address, which is used to receive data from other clients:

```javascript
console.log(client.addr);
```

Listen for connection established:

```javascript
client.on('connect', () => {
  console.log('Connection opened.');
});
```

Send data to other clients:

```javascript
client.send(
  'another client address',
  'some message',
);
```

Receive data from other clients:

```javascript
client.on('message', (src, payload) => {
  console.log(src, payload);
});
```

Check [examples](examples) for full examples.

## Contributing

**Can I submit a bug, suggestion or feature request?**

Yes. Please open an issue for that.

**Can I contribute patches?**

Yes, we appreciate your help! To make contributions, please fork the repo, push
your changes to the forked repo with signed-off commits, and open a pull request
here.

Please sign off your commit. This means adding a line "Signed-off-by: Name
<email>" at the end of each commit, indicating that you wrote the code and have
the right to pass it on as an open source patch. This can be done automatically
by adding -s when committing:

```shell
git commit -s
```

## Community

* [Telegram](https://t.me/nknorg)
* [Reddit](https://www.reddit.com/r/nknblockchain/)
* [Twitter](https://twitter.com/NKN_ORG)
* [Facebook](https://www.facebook.com/nkn.org)
