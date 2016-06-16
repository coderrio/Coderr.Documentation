log4net installation
====================

You've just installed the log4net integration library for OneTrueError. All exceptions that are logged through log4net will automatically be uploaded to OneTrueError.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/onetrueerror/");
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
OneTrue.Configuration.CatchLog4NetExceptions();
```

It must be added after the log4net configuration, but before the first usage of `LogManager.GetLogger()`.


## More information

* [Client configuration](index.md)
* [Client API reference](http://onetrueerror.com/docs/api/client/log4net/)
* [Getting started guide](../../gettingstarted.md)
* [Install OneTrueError server](http://onetrueerror.com/download/server/)
