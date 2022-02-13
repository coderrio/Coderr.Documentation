Installation
========================

Install the NPM-package `coderr.client`.

In your entry point script, add the following:

```javascript
import { err } from "coderr.client";

// in the top of your entrypoint javascript
err.configuration.credentials("https://report.coderr.io", "yourAppKey", "yourSharedSecret");
``` 

That's it. 


Try to report an error:

```javascript
import { err } from "coderr.client";

try {
    // do something

} catch(e) {
    err.report(e);
}
```

For more configration and reporting options, read the [client documentation](index.md).