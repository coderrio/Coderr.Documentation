Getting started
================

# Prerequisites

This guide assumes that you have installed and configured one of our [nuget](https://www.nuget.org/packages?q=coderr.client) libraries.

You must also use our [codeRR Live](https://app.coderrapp.com) service or install the [codeRR Community Server](../server/installation.md).

## Simplest possible reporting

The `Err` class in the client library is the main API that you use when reporting errors to codeRR. At its simplest form it takes
a single argument, the exception that you want to report.

```csharp
try
{
    somelogic();
}
catch(SomeException ex)
{
	Err.Report(ex);
}
```

The exception should appear in your server instance shortly after being reported.

![](screenshot.png)

## Attaching context information

Usually an exception is not enough information alone to be able to understand why and how the exception was thrown. codeRR will
always collect a number of parameters for you. You might however have information that directly allows you to understand
why the exception was thrown.

That information can be attached when reporting:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex, yourContextData);
}
```

### Using anonymous object

If you need to attach multiple values you can use an anonymous object:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex, new { UserId = userId, UserState = state });
}
```

**Result**

![](anonymous-object.png)

### Custom collections

We also have an object overload which can transform any object into a context collection (one of the groups in the "Context Data" menu in our web site).

Below we are using `ToContextCollection()` extension method which can transform any object (including complex objects) into a context collection.


```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    var modelCollection = viewModel.ToContextCollection("ViewModel");
    var loggedInUser = User.ToContextCollection("User");
    Err.Report(ex, new[]{modelCollection, loggedInUser});
}
```

**Result**

![](attach_multiple_collections.png)

Hence you can easily attach and group your information just as you like.

## Categorize exceptions using tags

We automatically identify common StackOverflow.com tags when analyzing exceptions (to help you find answers by searching StackOverflow.com). You can
also add your own tags by adding a special property to any context collection named "ErrTags":

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    Err.Report(ex, new { ErrTags = "important,backend" });
}
```

**Result:**

![](tag-demo.png)

# More information

Each nuget library has its own unique features. You can find the documentation on the [client start page](index.md).
