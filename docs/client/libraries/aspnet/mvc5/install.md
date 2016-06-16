ASP.NET MVC 5 installation
====================

You've just installed the ASP.NET MVC 5 integration library for OneTrueError. 
All uncaught exceptions will automatically be uploaded to OneTrueError.

To get started add the following code to your application:

```
var url = new Uri("http://yourServer/onetrueerror/");

//keys can be found in your own OneTrueError installation
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");

OneTrue.Configuration.CatchMvcExceptions();
```


## More information

* [Client configuration](index.md)
* [Client API reference](http://onetrueerror.com/docs/api/client/aspnet/mvc5/)
* [Getting started guide](../../gettingstarted.md)
* [Install OneTrueError server](http://onetrueerror.com/download/server/)
