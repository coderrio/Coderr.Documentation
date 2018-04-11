log4net configuration
=====================

Install the nuget package called `coderr.client.log4net`, if you haven't already.

Next, you need to tell the Coderr library what server it should upload all error reports to.

Please add the following code in your `Program.cs` (or the starting point of the framework that you use).

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, 
                              "yourAppKey", 
                              "yourSharedSecret");
Err.Configuration.CatchLog4NetExceptions();
```

It must be added after the log4net configuration, but before the first usage of `LogManager.GetLogger()`.

Try to log an exception to see if it works.

```csharp
try
{
    throw new Exception("Oooop");
}
catch (Exception ex)
{
    _logger.Error("Testing Coderr", ex);
}
```

The error should appear in the Coderr server shortly after being reported.

## More information

Read how you can [report errors manually](../../gettingstarted.md)