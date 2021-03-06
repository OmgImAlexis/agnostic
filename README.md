# agnostic [![NPM Module](https://img.shields.io/npm/v/agnostic.svg?style=flat)](https://www.npmjs.com/package/agnostic)

A library that allows other projects to be agnostic of particular http server implementation.

[![Linux Build](https://img.shields.io/travis/alexindigo/agnostic/master.svg?label=linux:0.12-6.x&style=flat)](https://travis-ci.org/alexindigo/agnostic)
[![MacOS Build](https://img.shields.io/travis/alexindigo/agnostic/master.svg?label=macos:0.12-6.x&style=flat)](https://travis-ci.org/alexindigo/agnostic)
[![Windows Build](https://img.shields.io/appveyor/ci/alexindigo/agnostic/master.svg?label=windows:0.12-6.x&style=flat)](https://ci.appveyor.com/project/alexindigo/agnostic)

[![Coverage Status](https://img.shields.io/coveralls/alexindigo/agnostic/master.svg?label=code+coverage&style=flat)](https://coveralls.io/github/alexindigo/agnostic?branch=master)
[![Dependency Status](https://img.shields.io/david/alexindigo/agnostic/master.svg?style=flat)](https://david-dm.org/alexindigo/agnostic)
[![bitHound Overall Score](https://www.bithound.io/github/alexindigo/agnostic/badges/score.svg)](https://www.bithound.io/github/alexindigo/agnostic)

<!-- [![Readme](https://img.shields.io/badge/readme-tested-brightgreen.svg?style=flat)](https://www.npmjs.com/package/reamde) -->

*Notice of change of ownership: Starting version 1.0.0 this package has changed it's owner and goals. Old version (0.0.0) is still available on npm via `npm install agnostic@0.0.0` or on [github](https://github.com/dtudury/agnostic). Thank you.*


| node / libs |  express | restify        | hapi                                         | http |
| :--         | :--      | :--            | :--                                          | :--  |
| v0.12       | 3.x, 4.x |  2.x, 3.x, 4.x | 8.x, 9.x, 10.x                               |  ✓   |
| io.js       | 3.x, 4.x |  2.x, 3.x, 4.x | 8.x, 9.x, 10.x                               |  ✓   |
| v4          | 3.x, 4.x |  2.x, 3.x, 4.x | 8.x, 9.x, 10.x, 11.x, 12.x, 13.x, 14.x, 15.x |  ✓   |
| v5          | 3.x, 4.x |  2.x, 3.x, 4.x | 8.x, 9.x, 10.x, 11.x, 12.x, 13.x, 14.x, 15.x |  ✓   |
| v6          | 3.x, 4.x |  2.x, 3.x, 4.x | 8.x, 9.x, 10.x, 11.x, 12.x, 13.x, 14.x, 15.x |  ✓   |


## Install

```
npm install --save agnostic
```

## Example

### Your Library

```javascript
var agnostic = require('agnostic');

module.exports = agnostic(myRequestHandler);

/**
 * Does cool things
 *
 * @param {EventEmitter} request - request object, mimicking IncomingMessage
 * @param {Function} respond - callback to respond to the request
 */
function myRequestHandler(request, respond)
{
  // do cool things
  // `request.body` - parsed request body
  // `request.query` - parsed query string
  // `respond` is a function with the following signature:
  // `respond([code], [content[, options]]);`
  respond(200, 'Received hit to ' + request.url, {headers: {'X-Powered-By': 'AllCoolThings'}});
}
```

### Express [![express](https://img.shields.io/badge/express-3.x--4.x-brightgreen.svg?style=flat)](http://expressjs.com)

```javascript
var express = require('express');
var coolLib = require('above-cool-lib');

var app = express();

app.all('/my-endpoint', coolLib);

// start the server
app.listen(1337);
```

### Restify [![restify](https://img.shields.io/badge/restify-2.x--4.x-brightgreen.svg?style=flat)](http://restify.com)


```javascript
var restify = require('restify');
var coolLib = require('above-cool-lib');

var server = restify.createServer();

server.get('/my-endpoint', coolLib);
server.post('/my-endpoint', coolLib);

// start the server
server.listen(1337);
```

### Hapi [![hapi](https://img.shields.io/badge/hapi-8.x--15.x-brightgreen.svg?lstyle=flat)](http://hapijs.com)

```javascript
var Hapi = require('hapi');
var coolLib = require('above-cool-lib');

var server = new Hapi.Server();

// setup hapi server
server.connection({ port: 1337 });

server.route({
  method : ['GET', 'POST'], // Hapi uses GET handler for HEAD requests
  path   : '/my-endpoint',
  handler: coolLib
});

// start the server
server.start();

```

### http [![http](https://img.shields.io/badge/http-0.12.x--6.x-brightgreen.svg?style=flat)](https://nodejs.org/api/http.html)

```javascript
  var http    = require('http');
  var coolLib = require('above-cool-lib');

  server = http.createServer(coolLib);

  // start the server
  server.listen(1337);
```

## Want to Know More?

More examples can be found in [test folder](test/).

Or open an [issue](https://github.com/alexindigo/agnostic/issues) with questions and/or suggestions.

## License

Agnostic is released under the [MIT](LICENSE) license.
