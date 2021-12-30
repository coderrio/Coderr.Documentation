log4net integration
================

The log4net library injects Coderr into the logging pipeline of log4net. So each time you log something and include an exception, it's reported to Coderr. It's by far the easiest way to use the power of Coderr in legacy applications (which use log4net).


![](/screens/libraries/log4net/contextinfo.png)

Coderr will also automatically attach the latest log entries each time an error is reported through Coderr.


![](/screens/libraries/log4net/logs.png)

# Setup

You need to have installed the Coderr server somewhere and created an application in it. Once you've done that, you'll have an `appKey` and a `sharedSecret` which you can configure below.

Add the following code somewhere before the first logger is retrieved.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");

// This activates it.
Err.Configuration.CatchLog4NetExceptions();
```

***It must be added after the log4net configuration, but before the first usage of `LogManager.GetLogger()`.***


That's it. 

# Links

[Getting started guide](/getting-started.md)
