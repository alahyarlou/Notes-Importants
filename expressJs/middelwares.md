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
