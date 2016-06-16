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

*(this library requires that you have installed a OneTrueError server somewhere)*

## More information

* [ASP.NET client](index.md)
* [Client reporting](../index.md)
* [Server guide](../../server.md)
