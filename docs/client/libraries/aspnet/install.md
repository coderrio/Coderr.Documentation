asp.net installation
====================

You've just installed the ASP.NET integration library for OneTrueError. 
All uncaught exceptions will automatically be uploaded to OneTrueError.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/onetrueerror/");
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
OneTrue.Configuration.CatchAspNetExceptions();
```

## More information

* [ASP.NET client configuration](index.md)
* [ASP.NET client API reference](http://onetrueerror.com/docs/api/client/aspnet/)
* [Getting started guide](../../gettingstarted.md)
* [Install OneTrueError server](http://onetrueerror.com/download/server/)
