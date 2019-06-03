Client library documentation
============


Coderr cannot discover errors nor collect information about unless one of Coderr nuget packages are installed.

## Core libraries

Core libraries takes care of reporting errors to the Coderr server. Uploads are queued to not affect your application. You do typically not need to installed them manually, they are included when you install one of the automation packages.

There are two core libraries, [Coderr.Client](https://coderr.io/documentation/client/libraries/core/) (.NET 4.x base library) and [Coderr.Client.NetStd](https://coderr.io/documentation/client/libraries/netstd/install.md) (.NET Standard 1.6 and above). 

You can use them directly if you do not want to take advantage of our automation libraries.

## Automation libraries

Coderr can detect and report all unhandled exceptions (and other types of errors), along with information about why the exception was thrown. Once installed, Coderr will detect exceptions and collect information related to the error like HTTP requests, screenshots, view models and more. The goal is to make it easy to understand why an exception was thrown.


Name | Description
--- | -----
[Coderr.client](libraries/core/index.md) | Our reporting library, allows you to manually report exceptions.
[Coderr.client.netstd](libraries/netstd/index.md) | Our reporting library for .NET Standard 1.6 and above. Allows you to manually report exceptions.
[Coderr.client.aspnet](libraries/aspnet/index.md) | Generic ASP.NET library. Catches all unhandled exceptions and report them. Collects information about the HTTP request, session data etc. Allows you to easily create custom error pages for different HTTP error codes.
[Coderr.client.aspnet.mvc5](libraries/aspnet-mvc5/index.md) | ASP.NET MVC5 specific library. Does the same as the ASP.NET library, but do also collect specific MVC5 information like route data, ViewBag etc. Also allows you to customize your error pages by just creating them in the correct folder.
Coderr.client.aspnet.webapi2 | ASP.NET WebApi2 integration. Tracks exceptions, failed authentication attempts, invalid POSTs and other cool stuff.
[Coderr.client.aspnetcore.mvc](libraries/aspnetcore-mvc/) | Core MVC integration. Tracks exceptions, failed authentication attempts, invalid POSTs and other cool stuff.
Coderr.client.wcf | Catches unhandled exceptions in the WCF pipeline. Collects WCF specific information like the inbound WCF message that failed to be processed.
[Coderr.client.log4net](libraries/log4net/index.md) | Reports all exceptions that you log, including the error message that you wrote.
[Coderr.client.winforms](libraries/winforms/index.md) | Reports all unhandled exceptions. Can take screen shots and collect the state of all open forms.
[Coderr.client.WPF](libraries/wpf/index.md) | Reports all unhandled exceptions. Can take screen-shots and collect the state of all open windows and includes the state of all your active view models.

If your favorite library isn't listed, you can either create your own or use the core library (`Coderr.client`) to report exceptions



When you start using Coderr, it's typically not crucial that you log relevant information using your logging library, as Coderr typically includes all information that you need to understand the error.

To get help to install and configure our nuget libraries, read the  article below.

[Using the client libraries](https://coderr.io/documentation/client/)
[Reporting errors](https://coderr.io/documentation/)

The client libraries are only used to detect unhandled exceptions and to allow you to manually report exceptions.
They also collect context information and make sure that the error report is uploaded properly.

You need to either [install Coderr Community Edition](../server/installation/) or create an account in [Coderr Live](https://coderr.io/live/).

# Getting started

Our [Getting started](/) shows how you install and configure the client libraries and how you can report exceptions and attach custom context collections (like including method arguments or view models).

# Extending

Learn how you can create your own context collections and build your own client library.

[Extending](extending/)

# Integration libraries

We currently have integrations for the following .NET libraries: