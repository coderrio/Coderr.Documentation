Getting started
================

Welcome to the getting started guide.

## Presequites

* If you have not done it yet, you can download one of our libraries from [nuget](https://www.nuget.org/packages?q=onetrueerror.client).
*  [Install](../server/installation.md) the server.

## Using the client library

The first thing you need to do is to tell where the uploads should be sent and which application the reports are for.
The URL should point on your local server installation. The appKey and sharedSecret can be found in your OneTrueError server web site.

Once the above steps are completed you can configure the library like this:

```csharp
var url = new Uri("http://yourServer/onetrueerror/");
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
```

The easiest way to report an exception is like this:

```csharp
try
{
    somelogic();
}
catch(SomeException ex)
{
	OneTrue.Report(ex);
}
```

The exception should appear in your server installation shortly after being reported.

![](screenshot.png)

## Attaching context information

Usually an exception is not enough information alone to be able to understand why and how the exception was thrown. OneTrueError will
always collect a large number of parameters for you. You might however have information that directly allows you to understand
why the exception was thrown.

That information can be attached when reporting:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    OneTrue.Report(ex, yourContextData);
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
    OneTrue.Report(ex, new { UserId = userId, UserState = state });
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
    OneTrue.Report(ex, new[]{modelCollection, loggedInUser});
}
```

**Result**

![](attach_multiple_collections.png)

Hence you can easily attach and group your information just as you like.

## Categorize exceptions using tags

We automatically identify common StackOverflow.com tags when analyzing exceptions (to help you find answers by searching StackOverflow.com). You can
also add your own tags by adding a special property to any context collection named "OneTrueTags":

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    OneTrue.Report(ex, new { OneTrueTags = "important,backend" });
}
```

**Result:**

![](tag-demo.png)

# More information

You can read more about the features for the specific libraries from the [client start page](index.md)
