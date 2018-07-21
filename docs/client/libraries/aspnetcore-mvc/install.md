ASP.NET Core MVC configuration
==============================

Install the nuget package called `coderr.client.aspnetcore.mvc`, if you haven't already.

Next, you need to tell the Coderr library what server it should upload all error reports to.

Add the following code in your `Program.cs`:

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

The appKey and the sharedSecret can be found in the Coderr server under the following menu option:

![](../server_settings.png)

Select the correct application in the top left menu and then click on the "Configure your application" option.

To get Coderr to automatically report all unhandled exceptions you need to add the following in `Startup.cs`:

For OWIN errors:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // to catch errors that are not in the MVC pipeline
    app.CatchOwinExceptions();

    // [... rest of the code ...]
}
```

For MVC specific errors:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options =>
    {
        // for Coderr
        options.CatchMvcExceptions();
    });
}
```

Once configured, start your application and try manually to report an exception.

You can for example add the following code somewhere and then invoke a controller action:

```csharp
try
{
    throw new Exception("Hello world");
}
catch (Exception ex)
{
    Err.Report(ex, new { SampleData = "Context example"});
}
```

## More information

The MVC library can report all invalid model states, track failed login attempts and more. For additional configuration options and to learn more about this library, read the [ASP.NET Core MVC client documentation](index.md) 

To learn more about manually reporting errors, read our [reporting guide](../../gettingstarted.md).
