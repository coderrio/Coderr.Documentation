ASP.NET Core MVC configuration
==============================

This installation guide only activates the minimal amount of features, read the full guide at the bottom for more details.

Install the nuget package called `coderr.client.aspnetcore.mvc`..

## Activating Coderr

Add the following code in your `Program.cs`:

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

The appKey and the sharedSecret are found in the Coderr server under the managed application.

## Detecting errors

To get Coderr to automatically report all unhandled exceptions add the following in `Startup.cs`:

For Middleware errors, add the following to the `Configure` method:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // to catch errors that are not in the MVC pipeline
    app.CatchMiddlewareExceptions();

    // To get ASP.NET Cores logs attached:
    loggerFactory.AddCoderrProvider();

    // [... rest of the code ...]
}
```

For MVC specific errors:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // For newer versions, this method is named "AddControllersWithViews".
    services.AddMvc(options =>
    {
        // To activate Coderr
        options.CatchMvcExceptions();
    });
}
```

## Trying it out
Once configured, start your application and try manually to report an exception.

You can test by adding the following code in a controller action:

```csharp
try
{
    throw new Exception("Hello world");
}
catch (Exception ex)
{
    // Using "this." is required for automatically collected telemetry data.
    this.Report(ex, new { SampleData = "Context example"});
}
```

## More information

The MVC library can report all invalid model states, track failed login attempts, and more. For additional configuration options and to learn more about this library, read the [ASP.NET Core MVC client documentation](index.md) 

To learn more about manually reporting errors, read our [reporting guide](../../gettingstarted.md).
