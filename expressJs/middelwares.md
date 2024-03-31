# Middelwares

### What's middelwares?

Simply consider it as an entry way that requests must pass through here first and then reach the Handler.

In Express, in order to be able to write a middleware, we use the following method:

```js
app.use(path, callbak);
```

This method takes an optional parameter (path) and a requirement parameter (callback).

`example:`

```js
//instantiate the Express.js app
app.use("/admin", function (req, res, next) {
  console.log("%s %s — %s", new Date().toString(), req.method, req.url);
  return next();
});
//implement server routes

app.get("admin/login", (req, res) => {
  // TODO
});
```

Now, every request that passes through the `/admin` route, this log will be printed first.

_Middleware has many uses, for example, they can be used to `limit access` levels._

### Morgan Middelware in ExpressJs

```bash
npm install --save morgan
```

We can track all requests sent to the backend with this package,from which IP or when this request was sent

```js
const express = require("express");
const morgan = require("morgan");
app = express();

app.use(morgan(format:'combined'||'common'||'dev'||'short'||'tiny',options));
```

Using format string of predefined tokens:

```js
morgan(":method :url :status :res[content-length] - :response-time ms");
```

Function to determine if logging is skipped, defaults to false. This function will be called as skip(req, res):

```js
// EXAMPLE: only log error responses
morgan("combined", {
  skip: function (req, res) {
    return res.statusCode < 400;
  },
});
```

---

### CamelCase-Keys middelware

```bash
npm install camelcase-keys
```

```js
const express = require("express");
const camelcaseKey = (...args) =>
  import("camelcase-keys").then(({ default: camelcaseKeys }) =>
    camelcaseKeys(...args)
  );
app = express();

console.log(camelcaseKey("Foo-Bar"));

/* OUTPUT */

// fooBar
```

- Convert object Input:

```js
const camelcase = require("camelcase-input").camelcase;

console.log(camelcase({ "foo-bar": true }));

/* OUTPUT */
// { fooBar: true }
```

- Convert array of objects Input

```js
const camelcase = require("camelcase-input").camelcase;
console.log(camelcase([{ "foo-bar": true }, { is_that_you: true }]))[
  /* OUTPUT */
  ({ fooBar: true }, { isThatYou: true })
];
```

- Convert array of string Input

```js
const camelcase = require("camelcase-input").camelcase;
console.log(camelcase(["Foo-Bar", "are-you-there"]));
/* OUTPUT */
// fooBar, areYouThere
```

- Convert array of objects Input ({ deep: true })

```js
const camelcase = require('camelcase-input').camelcase
console.log(camelcase([{'FOo-bar': [{'abc-df__r': true}, {'tghd_dfdf--ee': true}]},
{'bar-foo': { 'Test-te': {'opt-tdt': 'dfdfdf'} }}],
{ deep: true })))

/* OUTPUT */
// [{ fooBar: [{ abcDfR: true }, { tghdDfdfEe: true }] },
//  { barFoo: { testTe: { optTdt: dfdfdf } } }]
```

### OmitEmpty middelware

```bash
$ npm install --save omit-empty
```

```js
const omitEmpty = require("omit-empty");

console.log(omitEmpty({ a: "a", b: "" }));
//=> { a: 'a' }

console.log(omitEmpty({ a: "a", b: { c: "c", d: "" } }));
//=> { a: 'a', b: { c: 'c' } }

console.log(omitEmpty({ a: ["a"], b: [] }));
//=> { a: ['a'] }

console.log(omitEmpty({ a: 0, b: 1 }));
//=> { a: 0, b: 1 }

// set omitZero to true, to evaluate "0" as falsey
console.log(omitEmpty({ a: 0, b: 1 }, { omitZero: true }));
//=> { b: 1 }
```
