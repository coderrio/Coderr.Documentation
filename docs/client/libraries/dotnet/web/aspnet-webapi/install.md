ASP.NET WebApi installation
===========================

Install the nuget package called `coderr.client.aspnet.webapi`.

Next, you need to tell the Coderr library what server it should upload all error reports to.

Add the following code in your `global.asax` or `Startup.cs`.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
```

To get automated error reporting, add the following:

```csharp
Err.Configuration.CatchWebApiExceptions();
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

The WebApi library can report all invalid model states, track failed login attempts and more.

If you want more information, read the  [ASP.NET WebApi documentation](index.md) or on error reporting  [report errors](../../gettingstarted.md)
