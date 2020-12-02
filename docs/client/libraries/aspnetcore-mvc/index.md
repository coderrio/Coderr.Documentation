ASP.NET Core MVC
================

This documentation is for the ASP.NET Core MVC library. You can find out other libraries [here](../).

This library will report all unhandled ASP.NET and MVC exceptions. It can also report if something goes too slow or if there are too many authentication failures.

# Prerequisites

You should also have installed and configured the ASP.NET Core MVC [nuget library](https://www.nuget.org/packages/Coderr.Client.AspNetCore.Mvc/).


# Customization options

There are some additional customization options to those above, that you can use in Coderr. Below we show how to track invalid model states, track slow requests, track authentication failures, report JavaScript errors and understand the included context collections in Coderr and ASP.NET.

If you are using Coderr Live, you can also configure the [prioritization](https://coderr.io/documentation/features/partitions/) feature.

## Tracking invalid model states

Invalid model states is a good indication of the quality of your user interface for reporting errors. If many of the users fail to submit forms properly, it clearly shows that they either don't know what they should enter, the forms are unclear or a combination thereof.

To activate invalid model states, simply add:

```csharp
Err.Configuration.TrackInvalidModelStates();
```

You will now get one incident reported per invalid form as shown below.

![](/screens/libraries/aspnetcore-mvc/modelstate-incident.png)

The collection itself contains the fields that was invalid as this:

![](/screens/libraries/aspnetcore-mvc/collections/modelstate.png)

## Tracking slow requests

Slow requests decrease the overall user experience. Coderr allows you to set the threshold for how long a request may take.

This is useful if you want to ensure that the application is responsive enough, whilst not doing performance monitoring.

To set a timing threshold, add the following configuration with your time limit:

```csharp
var maxTime = TimeSpan.FromMilliseconds(500);
Err.Configuration.TrackSlowRequests(maxTime);
```

![](slow-request-incident.png)

## Tracking authentication failures

Coderr can track all failed authentication attempts. If activated, this feature will report all requests with the `Authorization` header when getting a 401 as a response. [Learn more about HTTP authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication).

To activate tracking authentication failures, use the following line:

```
Err.Configuration.TrackAuthenticationFailures();
```

The example below shows how authentication failures are reported:

![](/screens/libraries/aspnetcore-mvc/authentication-incident.png)


## Report JavaScript errors

The ASP.NET Core MVC library can report JavaScript errors. Simply activate this feature, by including the built in script in your `_Layout.cshtml` like this:

```html
<script src="/coderr/js/"></script>
```

Now all unhandled JavaScript errors will be reported to Coderr, as follows:

![](/screens/libraries/aspnetcore-mvc/javascript-incident.png)

### JavaScript context collections

The following collections are included for JavaScript errors.

![](/screens/libraries/aspnetcore-mvc/js-collections/document.png)

![](/screens/libraries/aspnetcore-mvc/js-collections/window.png)

![](/screens/libraries/aspnetcore-mvc/js-collections/navigator.png)

![](/screens/libraries/aspnetcore-mvc/js-collections/screen.png)


## Included context collections in ASP.NET MVC.

These collections are included for all ASP.NET Core MVC exceptions.

### ActionDescriptor

Information about the action and why it was selected.

![](/screens/libraries/aspnetcore-mvc/collections/actiondescriptor.png)

### Form

Information supplied in the HTTP post.

![](/screens/libraries/aspnetcore-mvc/collections/form.png)

### HttpRequest

Properties from the `HttpRequest` object in MVC.

![](/screens/libraries/aspnetcore-mvc/collections/request.png)

### HttpRequestHeaders

ALL headers from the HTTP request.

![](/screens/libraries/aspnetcore-mvc/collections/httprequestheaders.png)

### ModelState

Did we receive a valid model?

![](/screens/libraries/aspnetcore-mvc/collections/modelstate.png)

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

![](/screens/libraries/aspnetcore-mvc/collections/tempdata.png)

### ViewData / ViewBag

The ViewBag and/or ViewData is collected if specified.

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

![](/screens/libraries/aspnetcore-mvc/collections/viewdata.png)


# Links

We have a guide for [reporting errors](../../) manually. Read it to get the most out of Coderr.

You can also attach your own context information by building a custom [context provider](https://coderr.io/documentation/client/extending/contextprovider/). 
