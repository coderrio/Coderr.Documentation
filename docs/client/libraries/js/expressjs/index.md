ExpressJS library
=================

Coderr provides automated error reporting for ExpressJS-based applications.

_this is a beta library, feel free to try it_

![](/screens/libraries/js/express/error.gif)

https://coderr.io

## Reporting slow queries.

You can report slow queries and/or all pages that generate 403 (Forbidden).

Add the coderrMiddleware for that:

```javascript
import * as coderr from "coderr.client.expressjs";

// Either use this to set a limit to all HTTP verbs (in milliseconds)
coderr.requestTimeThreshold = 200;

// or do it per verb:
coderr.requestMethodTimeThresholds['post'] = 200;

// As the *first* middleware:
app.use(coderr.coderrMiddleware);
```

## Reporting forbidden requests

You can report all requests that generate 403 forbidden:

```javascript
import * as coderr from "coderr.client.expressjs";

coderr.reportForbidden = true;

// As the *first* middleware:
app.use(coderr.coderrMiddleware);
```

## Further reading

* [Client reporting](index.md)
* [Getting started guide](https://coderr.io/documentation/getting-started)
