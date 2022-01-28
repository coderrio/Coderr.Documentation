Javascript library
==================

This library supports both browser (es6) and nodejs based applications. It can easily be compiled into IIFE to support older browsers too.

Read the [installation guide](installation.md) for help installing the library.

## Basic reporting

Once you have installed and configured the reporting library you can start reporting errors.

```javascript
import * as coderr from "coderr.client";

try {

    // do something

} catch(e) {
    coderr.report(e, { userId: 20});
}

``` 

If that is executed in a browser based application, you'll get the following error in Coderr:

![](/screens/libraries/js/core/error.gif)


The type of information attached to an error report depends on the type of error and in which framework/library the error is detected.

### Adding context data

As shown above, the second argument is used to attach data to error reports. Any type of information can be included.

```javascript
coderr.report(e, { userId: 20, address: { city: 'Falun' }});
``` 

![](/screens/libraries/js/core/complex-data.gif)

To include multiple sets of data, simply attach them as an array:

```javascript
coderr.report(e, [userInfo, orderInfo]);
``` 

However, make it easier to navigate data, format the sets of data as our own context collection structure:

```javascript
var collection  = {
    name: 'MyCollection',
    properties: {
        someName: 'someValue'
    }
}
coderr.report(e, collection);
```

![](/screens/libraries/js/core/some-collection.gif)

## Automated reporting

Coderr can attach more telemetry and make the reporting automated. For that, you need to install one of the framework libraries, like expressjs or the angular package.

## Configuration

You can adjust how Coderr handles errors. It's done with the help of the configuration object.

### Application version

Specify the application version in the error reports. By doing so, Coderr can ignore reports for errors that have been corrected in newer versions.

```javascript
import {config} from "coderr.client";

coderr.config.applicationVersion = "1.0";
```

### Environment

Errors during development are normally not necessary to track in Coderr, as you probably are aware of most of them.
To turn reporting off in some environments, you need to tell Coderr which environment the errors are from.

```javascript
import {config} from "coderr.client";

config.environmentName = 'Development';
```

Once one error has been reported, mute the environment in the Coderr UI (under application settings).

### Pre process error reports

Sometimes additional information has to be added to error reports (session data, tags, priority etc). Hook into the error reporting pipeline to do that.

Another typical use case is to remove sensitive data from the telemetry.

```csharp
import {config} from "coderr.client";

config.errorPreProcessor = context => {
    // just an example
    if (context.contextType == "DOM") {
        context.logEntries = browserLogger.entries;
    }
}
```

### Filter reports

You can prevent reports from being uploaded to Coderr.

```javascript
import {config} from "coderr.client";

config.filter.push({
    invoke(context: ReportFilterContext){
        if (context.report.Exception.Message === 'Hello'){
            context.canSubmitReport = false;
        }
    }
});
```

### Attaching telemetry to reports

You can add telemetry to all generated reports:

```csharp
config.providers.push({
    collect(context: coderr.contextCollections.IContextCollectionProviderContext){
        context.contextCollections.push({
            name: 'SomeInfo',
            properties: {
                "Starsystem": "Andromeda"
            }
        });
    }
});
```

There are different types of context classes. Each framework integration has its own. For instance, browser errors provide a DOM context where the `window` and the `document` are provided.

The `context.contextType` property specifies which context is used for the error that is currently being reported.

