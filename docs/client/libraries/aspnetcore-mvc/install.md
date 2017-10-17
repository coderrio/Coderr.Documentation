ASP.NET Core MVC configuration
==============================

If you have not done that yet, install the nuget package called `coderr.client.aspnetcore.mvc`.

Next, you need to tell the codeRR library what server it should upload all error reports to.

Add the following code in your `Program.cs`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

If you want codeRR to automatically report all unhandled exceptions you need to add this the following in `Startup.cs`:

For OWIN errors:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // to catch errors that are not in the MVC pipeline
    app.CatchOwinExceptions();

    // [... rest of the code ...]
}
```

For MVC errors:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc(options =>
    {
        // for codeRR
        options.CatchMvcExceptions();
    });
}
```

Once configure, start your application and try to report an exception.

You can for instance add the following code somewhere and then invoke your controller action:

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

The MVC library can report all invalid model states, track failed login attempts and more.

Want to dig deeper? Read the [ASP.NET Core MVC client documentation](index.md) or how you can [report errors](../../gettingstarted.md)
