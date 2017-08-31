Client library documentation
============

The client libraries are only used to detect unhandled exceptions and to allow you to manually report exceptions.
They also collect context information and make sure that the error report is uploaded properly.

You also need to either [install OneTrueError Community Edition](../server/installation.md) or create an account in [OneTrueError Live](https://onetrueerror.com/live/).

# Getting started

Our [Getting started](gettingstarted.md) shows how you install and configure the client libraries and how you can report exceptions and attach custom context collections (like including method arguments or view models).

# Extending

Learn how you can create your own context collections are build your own client library.

[Extending](extending/)

# Integration libraries

We currently have integrations for the following .NET libraries:

Name | Description
--- | -----
[OneTrueError.client](libraries/core/index.md) | Our reporting library, allows you to manually report exceptions.
[OneTrueError.client.aspnet](libraries/aspnet/index.md) | Generic ASP.NET library. Catches all unhandled exceptions and report them. Collects information about the HTTP request, session data etc. Allows you to easily create custom error pages for different HTTP error codes.
[OneTrueError.client.mvc5](libraries/aspnet/mvc5/index.md) | ASP.NET MVC5 specific library. Does the same as the ASP.NET library, but do also collect specific MVC5 information like route data, ViewBag etc. Also allows you to customize your error pages by just creating them in the correct folder.
OneTrueError.client.wcf | Catches unhandled exceptions in the WCF pipeline. Collects WCF specific information like the inbound WCF message that failed to be processed.
[OneTrueError.client.log4net](libraries/log4net/index.md) | Reports all exceptions that you log, including the error message that you wrote.
OneTrueError.client.winforms | Reports all unhandled exceptions. Can take screen shots and collect the state of all open forms.

If your favorite library isn't listed, you can either create your own or use the core library (`OneTrueError.client`) to report exceptions