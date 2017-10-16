ASP.NET MVC 5 installation
====================

You've just installed the ASP.NET MVC 5 integration library for codeRR. 
All uncaught exceptions will automatically be uploaded to codeRR.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");

Err.Configuration.CatchMvcExceptions();
```

AppKey/SharedSecret can be found in your own codeRR server installation.

## More information

* [ASP.NET MVC5 Quick start](index.md)
* [ASP.NET MVC5 API reference](https://coderrapp.com/docs/api/client/aspnet/mvc5/)
* [Getting started guide](../../../gettingstarted.md)
* [Server installation](https://coderrapp.com/documentation/server/installation.md)
