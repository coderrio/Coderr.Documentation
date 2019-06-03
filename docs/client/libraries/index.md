Client libraries
==================

## Base packages

These packages enables you to start reporting errors.
They do not report errors automatically.

They will be included automatically when you install one of our automation libraries.

Name | Description
--- | -----
[Coderr.client](libraries/core/index.md) | Base library for .NET 4.61
[Coderr.client.netstd](libraries/netstd/index.md) | Base library for .NET Standard 1.6 and above


## Automation packages


Name | Description
--- | -----
[Coderr.client.aspnet](libraries/aspnet/index.md) | ASP.NET 4 library. Collects information about the HTTP request, session data etc. Allows you to easily create custom error pages for different HTTP error codes.
[Coderr.client.aspnet.mvc5](libraries/aspnet-mvc5/index.md) | ASP.NET MVC5. Does the same as the ASP.NET library, but do also collect specific MVC5 information like route data, ViewBag etc. Also allows you to customize your error pages by just creating them in the correct folder.
Coderr.client.aspnet.webapi2 | ASP.NET WebApi2 integration. Tracks exceptions, failed authentication attempts, invalid POSTs and other cool stuff.
[Coderr.client.aspnetcore.mvc](libraries/aspnetcore-mvc/) | ASP.NET Core MVC. Tracks exceptions, failed authentication attempts, invalid POSTs and other cool stuff.
Coderr.client.wcf | Catches unhandled exceptions in the WCF pipeline. Collects WCF specific information like the inbound WCF message that failed to be processed.
[Coderr.client.log4net](libraries/log4net/index.md) | Reports all exceptions that you log, including the error message that you wrote.
[Coderr.client.winforms](libraries/winforms/index.md) | Reports all unhandled exceptions. Can take screen shots and collect the state of all open forms.
[Coderr.client.WPF](libraries/wpf/index.md) | Reports all unhandled exceptions. Can take screen-shots and collect the state of all open windows and includes the state of all your active view models.

If your favorite library isn't listed, you can either [create your own](../extending/) or use the core library (`Coderr.client`) to report exceptions.