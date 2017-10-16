log4net installation
====================

You've just installed the log4net integration library for codeRR. All exceptions that are logged through log4net will automatically be uploaded to codeRR.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
Err.Configuration.CatchLog4NetExceptions();
```

It must be added after the log4net configuration, but before the first usage of `LogManager.GetLogger()`.


## More information

* [Client configuration](index.md)
* [Client API reference](https://coderrapp.com/docs/api/client/log4net/)
* [Getting started guide](../../gettingstarted.md)
* [Install codeRR server](https://coderrapp.com/download/server/)
