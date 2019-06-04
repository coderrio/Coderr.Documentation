Client library documentation
============


Coderr cannot discover errors nor collect information about unless one of Coderr's nuget packages are installed.

## Core libraries

Core libraries takes care of reporting errors to the Coderr server. Uploads are queued to not affect your application. You do typically not need to installed them manually, they are included when you install one of the automation packages.

There are two core libraries, [Coderr.Client](https://coderr.io/documentation/client/libraries/core/) (.NET 4.x base library) and [Coderr.Client.NetStd](https://coderr.io/documentation/client/libraries/netstd/install.md) (.NET Standard 1.6 and above). 

You can use them directly if you do not want to take advantage of our automation libraries.

## Automation libraries

Coderr can detect and report all unhandled exceptions (and other types of errors), along with information about why the exception was thrown. The automation libraries can also report other kinds of errors like validation failures or slow requests.

Once installed, Coderr will detect exceptions and collect information related to the error like HTTP requests, screenshots, view models and more. The goal is to make it easy to understand why an exception was thrown without manual handling.


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

If your favorite library isn't listed, you can either create your own, request one in our [forum](https://discuss.coderr.io) or use the core library (`Coderr.client`) to report exceptions.

To get help to install and configure our nuget libraries, read the  article below.

The client library requires that a server is used. Install one or use our hosted service. [More information](../).


# Getting started

Our [Getting started](../getting-started/) guide shows how to install and configure the client libraries and how you can report exceptions and attach custom context collections (like including method arguments or view models).

# Controlling report uploads

Reports that fail to upload are thrown away by default, to avoid interfering with your application.

To enable queued report uploads, use the following configuration line to activate it:

```csharp
Err.Configuration.QueueReports = true;
```

When reports are being uploaded, the queue makes sure that your UI-unresponsiveness is unaffected.

There is more information about how to control the error report uploads in our [customizing uploads guide](customize-uploads).

## Adding your own automated context providers

In your own application you probably have system specific information that you always want to include when errors are reported. For example `tenantId`,  `customerId` or the logged-in user.

That can be done by creating a [Context Data Provider](extending/contextprovider)

# Building a new library

Learn how you can build your own client library for your own favorite .NET project.

[New client library](extending/clientlib)
