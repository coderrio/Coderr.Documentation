ExpressJS installation
========================

Download this package:

```js
npm -I coderr.client.expressjs
```

Import both the Coderr base library and the expressjs package:

```javascript
import { err } from "coderr.client";
import { activatePlugin, errorMiddleware } from "coderr.client.expressjs";

// in the top of your app.js/ts
err.configuration.credentials("https://report.coderr.io", "yourAppKey", "yourSharedSecret");

// To configure the expressJS plugin.
activatePlugin(err);

// As the last middleware:
app.use(errorMiddleware);

```

To learn how to use the library, read the [client documentation](index.md).