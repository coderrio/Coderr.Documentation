log4net integration
================

The log4net library injects codeRR into the logging pipeline of log4net. Each time you log something and include an exception it will be reported to codeRR. This is by far the easiest way to use the power of codeRR in legacy applizations (which use log4net).

# Setup

You need to have installed the codeRR server somewhere and created an application in it. Once you've done that you'll have a `appKey` and a `sharedSecret` which you can configure below.

Add the following code somewhere before the first logger is retrieved.

```
var url = new Uri("http://yourServer/coderr/");
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
OneTrue.Configuration.CatchLog4NetExceptions();
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
	_logger.Debug("Failed doing some crazy stuff.", ex);
}
```

.. the exception will be picked up in codeRR.

As a bonus you will also see information about the log entry in codeRR:

![](contextinfo.png)

# Links

* [Client API reference](http://coderrapp.com/docs/api/client/log4net/)
* [Getting started guide](../../gettingstarted.md)
