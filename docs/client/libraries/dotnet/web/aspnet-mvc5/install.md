ASP.NET MVC 5 configuration
===========================

Install the nuget package called `coderr.client.aspnet.mvc5`, if you haven't already.

Next, you need to tell the Coderr library what server it should upload all error reports to.

PLease add the following code in your `global.asax` or `Startup.cs`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

To get Coderr to automatically report all unhandled exceptions you need to add the following in `global.asax` or `Startup.cs`:

```csharp
Err.Configuration.CatchMvcExceptions();
```

Once configured, start your application and try manually to report an exception.

You can for example add the following code somewhere and then invoke your controller action:

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

If you want more information, read the  [ASP.NET Mvc5 client documentation](index.md) or on error reporting  [report errors](../../gettingstarted.md)
