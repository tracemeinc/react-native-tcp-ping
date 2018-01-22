tcp-ping
========

TCP ping utility for node.js. You can test if chosen address accepts connections at desired port and find out your latency. Great for service availability testing.

#####Why not ```ping``` wrapper?

* It's much faster than ```ping``` tool (as soon as connection gets accepted, it's dropped and a new measure is conducted immediately), so there's no unnecessary waiting between requests.
* It allows you to test a specific service, not the whole connection
* Some servers drop ICMP echo without any response, even when online. TCP can work in such cases.

###Install

```
npm install tcp-ping
```

###Functions

#####ping(options)

```options``` is an object, which may contain several properties:

* address (address to ping; defaults to ```localhost```)
* port (defaults to ```80```)
* timeout (in ms; defaults to 5s)
* attempts (how many times to measure time; defaults to 10)

Returns a promise that resolves with an object which looks like this:
```javascript
{
  address: '46.28.246.123',
  port: 80,
  attempts: 10,
  avg: 19.7848844,
  max: 35.306233,
  min: 16.526067,
  results:
   [
    { seq: 0, time: 35.306233 },
    { seq: 1, time: 16.585919 },
    ...
    { seq: 9, time: 17.625968 }
   ]
}
```

#####probe(address, port)

###Usage

```javascript
var tcpp = require('react-native-tcp-ping');

const available = await tcpp.probe('46.28.246.123', 80)

const data = await tcpp.ping({ address: '46.28.246.123' })
```
