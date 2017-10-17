ASP.NET MVC 5 configuration
===========================

If you have not done that yet, install the nuget package called `coderr.client.aspnet.mvc5`.

Next, you need to tell the codeRR library what it should upload all error reports to.

Add the following code in your `global.asax` or `Startup.cs`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

If you want codeRR to automatically report all unhandled exceptions you need to add this line too:

```csharp
Err.Configuration.CatchMvcExceptions();
```

Once done, try to report an exception.

Add the following somewhere and then invoke your application:

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

The MVC library also includes custom error pages and other goodies.

Want to dig deeper? Read the [ASP.NET Mvc5 client documentation](index.md) or how you can [report errors](../../gettingstarted.md)
