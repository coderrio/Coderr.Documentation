Client library documentation
============

Welcome to the OneTrueError client library documentation.

* [Getting started](gettingstarted.md)
* [Extending](extending/)


# Integration libraries

Name | Description
--- | -----
[OneTrueError.client](libraries/core/index.md) | Our reporting library, allows you to manually report exceptions.
[OneTrueError.client.aspnet](libraries/aspnet/index.md) | Generic ASP.NET library. Catches all unhandled exceptions and report them. Collects information about the HTTP request, session data etc. Allows you to easily create custom error pages for different HTTP error codes.
[OneTrueError.client.mvc5](libraries/aspnet/mvc5/index.md) | ASP.NET MVC5 specific library. Does the same as the ASP.NET library, but do also collect specific MVC5 information like route data, ViewBag etc. Also allows you to customize your error pages by just creating them in the correct folder.
OneTrueError.client.wcf | Catches unhandled exceptions in the WCF pipeline. Collects WCF specific information like the inbound WCF message that failed to be processed.
[OneTrueError.client.log4net](libraries/log4net/index.md) | Reports all exceptions that you log, including the error message that you wrote.
OneTrueError.client.winforms | Reports all unhandled exceptions. Can take screen shots and collect the state of all open forms.
