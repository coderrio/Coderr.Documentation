ASP.NET Integration
======================

This library is intended for ASP.NET projects that are not using MVC.

# Setup

You need to have installed the OneTrueError server somewhere and created an application in it. Once you've done that you'll have a `appKey` and a `sharedSecret` which you can configure below.

Add the following code in `global.asax`:

```
var url = new Uri("http://yourServer/onetrueerror");
OneTrue.Configuration.Credentials(url, "13d82df603a845c7a27164c4fec19dd6", "6f0a0a7fac6d42caa7cc47bb34a6520b");
OneTrue.Configuration.CatchAspNetExceptions();
```

All unhandled exceptions will now be reported.

# Customizations

This section describes how you can customize the built in features. You can also add your own [context providers](../../extending/contextprovider.md).

## Error pages

The library contains a custom error page which can be activated (and shown) when an exception is caught. 

To activate it add the following code:

```csharp
var provider = new VirtualPathProviderBasedGenerator("~/Errors/");
OneTrue.Configuration.SetErrorPageGenerator(provider);
```

The code says that the library should look after error pages (either `.aspx` or  `.html`) in the specified folder:

![](error-folder.png)

The library tries to find pages based on the HTTP code. If the code is 404 the library tries to find the following error pages:

1. FileNotFound.aspx
2. FileNotFound.html
3. Error.aspx
4. Error.html

That is, it tries to find a specific file first. If a specific file do not exist it tries to load a generic one.

### Error information

TO get information into your view, simply declare one of the following properties in your code behind.

---------------------------------
| Property | Type | Description |
|------|----|----|
|ErrorContext | HttpErrorReporterContext | Look in the Client API specification for more information |
|Exception | *Exception* | The caught exception |
-------------------------------

If you are just using HTML you can use the following template strings:

---------------------------------
| Template text | Description |
|------|----|----|
|`{ErrorMessage}` | Exception message |
-------------------------------

# Links

* [Client API reference](http://onetrueerror.com/docs/api/client/aspnet/)
* [Getting started guide](../../gettingstarted.md)
