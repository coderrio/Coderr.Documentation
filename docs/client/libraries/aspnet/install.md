ASP.NET configuration
=====================

To start with, you need to tell the codeRR library what it should upload all error reports to.

Add the following code in your `global.asax`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
```

If you want codeRR to automatically report all unhandled exceptions you need to add this line too:

```csharp
Err.Configuration.CatchAspNetExceptions();
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

## More information

The ASP.NET library also includes custom error pages and other goodies.

Want to dig deeper? Read the [ASP.NET client documentation](index.md) or how you can [report errors](../../gettingstarted.md)
