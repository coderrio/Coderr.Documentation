ASP.NET Core MVC
================

This library reports all unhandled ASP.NET exceptions; from both MVC and custom middlewares. It can also report if requests go too slow or if there are too many authentication failures. 

![](/screens/libraries/aspnetcore-mvc/error.png)

# Configuration options

Besides only reporting exceptions, Coderr can report additional types of errors.

## Tracking invalid model states

Invalid model states are a good indication of the UX quality. For example, if many users fail to submit forms correctly, it clearly shows that they either don't know what they should enter, the forms are unclear or, a combination thereof.

To activate invalid model states, add:

```csharp
Err.Configuration.TrackInvalidModelStates();
```

Example error

![](/screens/libraries/aspnetcore-mvc/modelstate.png)


## Tracking slow requests

Slow requests decrease the overall user experience. Let Coderr report all requests that are too slow.

Add the following line with your time-limit:

```csharp
var maxTime = TimeSpan.FromMilliseconds(500);
Err.Configuration.TrackSlowRequests(maxTime);
```

![](slow-request-incident.png)

## Tracking authentication failures

Coderr can track all failed authentication attempts. If activated, this feature will report all requests with the `Authorization` header when getting a 401 or 403 as a response. [Learn more about HTTP authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication).

To activate tracking authentication failures, use the following line:

```
Err.Configuration.TrackAuthenticationFailures();
```

The example below shows how authentication failures are reported:

![](authentication-incident.png)


## Reporting javascript errors

The ASP.NET Core MVC library can report javascript errors. The built in JS error detector is minimalistic, you can of course use our NPM package instead, which is more feature complete.

Simply activate this feature, by including the built in script in your `_Layout.cshtml` like this:

```html
<script src="/coderr/js/"></script>
```

All unhandled javascript errors are now reported to Coderr, as follows:

![](javascript-incident.png)

### Javascript context collections

![](/screens/libraries/aspnetcore-mvc/js-collections.gif)

## Included context collections in ASP.NET.

![](/screens/libraries/aspnetcore-mvc/collections.gif)


Coderr can include the following information:

* Action descriptor
* Form data
* HttpRequest
* HttpRequest headers
* ModelState
* TempData
* ViewBag

# Links

* [Reporting errors](/features/reporting)
* [Getting started](/getting-started/)
