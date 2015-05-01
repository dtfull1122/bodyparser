koa-bodyparser
===============

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Coveralls][coveralls-image]][coveralls-url]
[![David deps][david-image]][david-url]
[![node version][node-image]][node-url]
[![Gittip][gittip-image]][gittip-url]

[npm-image]: https://img.shields.io/npm/v/koa-bodyparser.svg?style=flat-square
[npm-url]: https://npmjs.org/package/koa-bodyparser
[travis-image]: https://img.shields.io/travis/koajs/bodyparser.svg?style=flat-square
[travis-url]: https://travis-ci.org/koajs/bodyparser
[coveralls-image]: https://img.shields.io/coveralls/koajs/bodyparser.svg?style=flat-square
[coveralls-url]: https://coveralls.io/r/koajs/bodyparser?branch=master
[david-image]: https://img.shields.io/david/koajs/bodyparser.svg?style=flat-square
[david-url]: https://david-dm.org/koajs/bodyparser
[node-image]: https://img.shields.io/badge/node.js-%3E=_0.11-green.svg?style=flat-square
[node-url]: http://nodejs.org/download/
[gittip-image]: https://img.shields.io/gittip/dead-horse.svg?style=flat-square
[gittip-url]: https://www.gittip.com/dead-horse/


a body parser for koa, base on [co-body](https://github.com/tj/co-body).

## Install

[![NPM](https://nodei.co/npm/koa-bodyparser.png?downloads=true)](https://nodei.co/npm/koa-bodyparser/)

## Usage

```js
var koa = require('koa');
var bodyParser = require('koa-bodyparser');

var app = koa();
app.use(bodyParser());

app.use(function *() {
  // the parsed body will store in this.request.body
  // if nothing was parsed, body will be an empty object {}
  this.body = this.request.body;
});
```

## Options

* **encode**: requested encoding. Default is `utf-8` by `co-body`
* **formLimit**: limit of the `urlencoded` body. If the body ends up being larger than this limit, a 413 error code is returned. Default is `56kb`
* **jsonLimit**: limit of the `json` body. Default is `1mb`
* **detectJSON**: custom json request detect function. Default is `null`
  ```js
  app.use(bodyparser({
    detectJSON: function (ctx) {
      return /\.json$/i.test(ctx.path);
    }
  }));
  ```
* **extendTypes**: support extend types:
  ```js
  app.use(bodyparser({
    extendTypes: {
      json: ['application/x-javascript'] // will parse application/x-javascript type body as a JSON string
    }
  }));
  ```
* **onerror**: support custom error handle, if `koa-bodyparser` throw an error, you can customize the response like:
  ```js
  app.use(bodyparser({
    onerror: function (err, ctx) {
      ctx.throw('body parse error', 422);
    }
  }));
  ```
## Licences

[MIT](LICENSE)
