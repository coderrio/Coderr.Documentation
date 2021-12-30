nlog integration
================

The nlog library injects Coderr into the logging pipeline of nlog. So each time you log something and include an exception, it's reported to Coderr. It's by far the easiest way to use the power of Coderr in legacy applications (which use nlog).


![](/screens/libraries/nlog/error.png)

Coderr will also automatically attach the latest log entries each time an error is reported through Coderr.


![](/screens/libraries/nlog/logs.png)

# Setup

You need to have installed the Coderr server somewhere and created an application in it. Once you've done that, you'll have an `appKey` and a `sharedSecret` which you can configure below.

Add the following code somewhere before the first logger is retrieved.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");

// This line must appear before the first call to LogManager.GetCurrentClassLogger()
// but after the logging configuration have been made.
Err.Configuration.CatchNLogExceptions();
```


## Usage

If you have code like this:

```csharp
try
{
	methodThatWillThrowAnException();
}
catch (Exception ex)
{
	_logger.Debug("Failed to do some crazy stuff.", ex);
}
```

.. the exception is now reported to  Coderr.

# Links

[Getting started guide](/getting-started.md)
