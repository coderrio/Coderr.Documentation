ASP.NET WebApi
===============

This documentation is for the ASP.NET WebApi library. You can find out other libraries [here](../).

This library will report all unhandled ASP.NET WebApi exceptions. It can also report if something goes too slow or if there are too many authentication failures.

# Prerequisites

You should have installed [Coderr.Client.AspNet.WebApi](https://www.nuget.org/packages/Coderr.Client.AspNet.WebApi/) and done the base configuration (specified credentials for Coderr).

# Getting started

To activate the automated reporting, add this to your `WebApiConfig` in the `App_Start` folder.

```csharp
// This is the base configuration for coderr.
// Change the URL if you are using Coderr Premise or Coderr Community.
var url = new Uri("https://report.coderr.io/");
Err.Configuration.Credentials(url,
    "yourAppKey",
    "yourSharedSecret");

Err.Configuration.CatchWebApiExceptions(config);
```

Once done, try to throw an exception in one of your WebApi controllers.

# Tracking performance

Making sure that requests are processed quickly can be important. Coderr allows you to report slow requests with a simple configuration:

```csharp
Err.Configuration.TrackPerformance(x =>
{
    // Everything under 500ms is ok.
    if (x.ExecutionTime.TotalMilliseconds < 500) return;

    // GET requests must be faster than 500ms.
    if (x.Request.Method == HttpMethod.Get)
    {
        x.ReportRequest();
    }

    // POSTs most be faster than 2 seconds.
    if (x.Request.Method == HttpMethod.Post && x.ExecutionTime.TotalMilliseconds > 2000)
    {
        x.ReportRequest();
    }
});
```

Your can of course set different requirements for different areas in your web site.

Example error message from Coderr:

> *Slow Request 'Values.Get' took 51970ms*

# Logging

Coderr will automatically include the 100 latest log entries from the ASP.NET WebApi tracing functionality. You can fine tune that using the `ConfigureLogging` method.

```csharp
Err.Configuration.ConfigureLogging(options =>
{
    options.MaxAge = TimeSpan.FromMinutes(2);
    options.MinLevel = TraceLevel.Info;
    options.MaxEntries = 50;
});
```

![](/screens/libraries/aspnet-webapi/logs.png)
