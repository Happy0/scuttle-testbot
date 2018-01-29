# scuttle-testbot

> Spins up an empty, temporary scuttlebot server that stores data in your temp folder


## Usage

```js
var CreateTestSbot = require('scuttle-testbot')
var ssbKeys = require('ssb-keys')

var pietKeys = ssbKeys.generate()
var katieKeys = ssbKeys.generate()

var myTempSbot = CreateTestSbot({name: 'testBotName', keys: pietKeys})

var katie = myTempSbot.createFeed(katieKeys)
var piet = myTempSbot.createFeed(pietKeys)

piet.add({type: 'test', content: "a test message"},function(err, data) {
  myTempSbot.close() //don't forget to close your sbot otherwise your script will never exit. ;)
  console.log(data)
})
```

Outputs:
```
{ 
  key: '%FQ2auS8kVY9qPgpTWNY3le/JG5+IlO6JHDjBIQcSPSc=.sha256',
  value: { 
    previous: null,
    sequence: 1,
    author: '@UreG2i/rf4mz7QAVOtg0OML5SRRB42Cwwl3D1ct0mbU=.ed25519',
    timestamp: 1517190039755,
    hash: 'sha256',
    content: { type: 'test', content: 'a test message' },
    signature: '0AxMJ7cKjHQ6vJDPkVNWcGND4gUwv2Z8barND5eha7ZXH/s5T0trFqcratIqzmhE3YJU2FY61Rf1S/Za2foLCA==.sig.ed25519' 
  },
  timestamp: 1517190039758 
}
```

## API

```js
var CreateTestSbot = require('scuttle-testbot')
```

```
CreateTestSbot(opts={})
```
Returns a scuttlebot instance.

By default, CreateTestSbot deletes an existing database of the same `name` before starting.

Valid `opts` keys include:

`name` (default: `ssb-test + Number(new Date)`) - `myTestName`: Sets the database in /tmp/myTestName 

`startUnclean` (default: `false`) - `true`: Don't delete an existing database before starting up.

`keys` (default: scuttle-testbot generates a new set of random keys) - `keys`: generated by ssb-keys.


```
CreateTestSbot.use(require('ssb-about'))
```

`CreateTestSbot.use` lets you add scuttlebot plugins. `use` can be chained the same as the scuttlebot api.

## Install

With [npm](https://npmjs.org/) installed, run

```
$ npm install scuttle-testbot
```

## Acknowledgments


## See Also

- [`noffle/common-readme`](https://github.com/noffle/common-readme)

## License

MIT

