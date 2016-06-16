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

*(this library requires that you have installed a OneTrueError server somewhere)*


## More information

* [More information](index.md)
* [General client reporting](../index.md)
* [Installing OneTrueError](http://onetrueerror.com/download/server/)
