Serilog integration
================

The Serilog library injects Coderr into the logging pipeline of Serilog. So each time you log something and include an exception, it's reported to Coderr. It's by far the easiest way to use the power of Coderr in legacy applications (which use Serilog).


![](/screens/libraries/serilog/error.png)

Coderr will also automatically attach the latest log entries each time an error is reported through Coderr.


![](/screens/libraries/serilog/logs.png)

# Setup

You need to have installed the Coderr server somewhere and created an application in it. Once you've done that, you'll have an `appKey` and a `sharedSecret` which you can configure below.

Add the following code somewhere before the first logger is retrieved.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");

Log.Logger = new LoggerConfiguration()
	.WriteTo.Console()
	.WriteTo.Coderr() // Add this one to your config
	.CreateLogger();
```

That's it. 

## Usage

If you have code like this:

```csharp
try
{
	methodThatWillThrowAnException();
}
catch (Exception ex)
{
	Log.Logger.Write(LogEventLevel.Error, ex, "Hello World!");
}
```

.. the exception is now reported to Coderr.

# Links

[Getting started guide](/getting-started.md)
