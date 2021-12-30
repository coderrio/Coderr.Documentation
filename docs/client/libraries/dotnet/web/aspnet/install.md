ASP.NET configuration
=====================

Install the nuget package called `coderr.client.aspnet`, if you haven't already.

Next, you need to tell the Coderr library what server it should upload all error reports to.

Please add the following code in your `global.asax`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

To get Coderr to automatically report all unhandled exceptions you need to add the following in `global.asax`.

```csharp
Err.Configuration.CatchAspNetExceptions();
```

Once configured, start your application and try manually to report an exception.

You can for example add the following code somewhere and then invoke your application:


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

The ASP.NET library can include all http request, session data, submitted form and more.

If you want more information, read the [ASP.NET client documentation](index.md) or on error reporting  [report errors](../../gettingstarted.md)
