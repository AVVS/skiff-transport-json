# Skiff rpc transport over json

Externalized transport for use with sombrero-node like clusters. Server and client
for tcp-based rpc network. Pass in class with functions that are supposed to be
called remotely. This is more traffic over skiff-transport-msgpack, but lower CPU
impact, so more messages can be transmitted over time.

## Install

`npm install skiff-transport-json -S`

## Usage

```js
var transport = require('skiff-transport-json');
var Server = require('some-server-module');
// assume it has methods `ping` and `pong`

// on node 1 that will execute actions
transport.listen(3212, '10.0.0.1', Server, function serverBinded(err, server) {
    if (err) {
        throw err;
    }

    // net server object
});

// on other nodes

var rpc = transport.connect(['ping', 'pong'], '10.0.0.1', 3212);
rpc.on('connect', function clientConnected(client) {
    client.ping(function (err, response) {
        // this was invoked on node 1
    });
});

```
