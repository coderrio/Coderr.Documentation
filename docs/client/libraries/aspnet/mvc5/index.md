ASP.NET MVC 5 Integration
=========================

This client library will provide both ASP.NET and MVC specific context information for OneTrueError.


# Features

The library apart from detect and upload uncaughts exceptions also provide the following features.

## Error pages

## Context collections

To learn more about the included ASP.NET specifc context collections like HTTP Request, [read here](../index.md)


### Controller

The controller name is collected.

Example:

![](collections/controller.png)

### RouteData

Information about the route that MVC took is collected.

Example:

![](collections/routedata.png)

### TempData

TempData is collected if set.

Example:

```csharp
TempData["DemoKey"] = new {
		Amount = 20000,
		Expires = DateTime.UtcNow.AddMinutes(5)
};
```

Result:

![](collections/tempdata.png)

### ViewData / ViewBag

The Viewbag and/or ViewData is collected if specified.

Example:

```csharp
ViewBag.Title = "Hello";
ViewBag.Model = new
{
	state = "Running",
	Collected = true
};
```

Result:

![](collections/viewdata.png)


# Links

* [Client API reference](http://onetrueerror.com/docs/api/client/aspnet/mvc5/)
* [Getting started guide](../../gettingstarted.md)

