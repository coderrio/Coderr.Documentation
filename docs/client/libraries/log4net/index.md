log4net integration
================

The log4net library injects Coderr into the logging pipeline of log4net. Each time you log something and include an exception it will be reported to Coderr. This is by far the easiest way to use the power of Coderr in legacy applications (which use log4net).

# Setup

You need to have installed the Coderr server somewhere and created an application in it. Once you've done that you'll have a `appKey` and a `sharedSecret` which you can configure below.

Add the following code somewhere before the first logger is retrieved.

```csharp
var url = new Uri("http://yourServer/coderr/");
Err.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
Err.Configuration.CatchLog4NetExceptions();
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

.. the exception will be picked up in Coderr.

As a bonus you will also see information about the log entry in Coderr:

![](/screens/libraries/log4net/contextinfo.png)

# Links

* [Client API reference](https://coderrapp.com/docs/api/client/log4net/)
* [Getting started guide](../../gettingstarted.md)
