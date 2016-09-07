ASP.NET MVC 5 installation
====================

You've just installed the ASP.NET MVC 5 integration library for OneTrueError. 
All uncaught exceptions will automatically be uploaded to OneTrueError.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/onetrueerror/");
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");

OneTrue.Configuration.CatchMvcExceptions();
```

AppKey/SharedSecret can be found in your own OneTrueError server installation.

## More information

* [ASP.NET MVC5 Quick start](index.md)
* [ASP.NET MVC5 API reference](http://onetrueerror.com/docs/api/client/aspnet/mvc5/)
* [Getting started guide](../../../gettingstarted.md)
* [Server installation](http://onetrueerror.com/documentation/server/installation.md)
