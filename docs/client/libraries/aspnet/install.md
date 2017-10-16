asp.net installation
====================

You've just installed the ASP.NET integration library for codeRR. 
All uncaught exceptions will automatically be uploaded to codeRR.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
Err.Configuration.CatchAspNetExceptions();
```

## More information

* [ASP.NET client configuration](index.md)
* [ASP.NET client API reference](https://coderrapp.com/docs/api/client/aspnet/)
* [Getting started guide](../../gettingstarted.md)
* [Install codeRR server](https://coderrapp.com/download/server/)
