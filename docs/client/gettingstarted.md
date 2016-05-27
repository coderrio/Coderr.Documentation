Getting started
================

If you have not done it yet, you can download one of our libraries from [nuget](https://www.nuget.org/packages?q=onetrueerror.client):

Name | Description
--- | -----
OneTrueError | Our reporting library, allows you to manually report exceptions.
OneTrueError.aspnet | Generic ASP.NET library. Catches all unhandled exceptions and report them. Collects information about the HTTP request, session data etc. Allows you to easily create custom error pages for different HTTP error codes.
OneTrueError.mvc5 | ASP.NET MVC5 specific library. Does the same as the ASP.NET library, but do also collect specific MVC5 information like route data, viewbag etc. Also allows you to customize your error pages by just creating them in the correct folder.
OneTrueError.wcf | Catches unhandled exceptions in the WCF pipeline. Collects WCF specific information like the inbound WCF message that failed to be processed.
OneTrueError.log4net | Reports all exceptions that you log, including the error message that you wrote.
OneTrueError.winforms | Reports all unhandled exceptions. Can take screen shots and collect the state of all open forms.

When you have installed the library you need to activate it. It's done with the help of the appKey/Shared secret that you get once you create an account at our [homepage](http://onetrueerror.com/account/register).

```csharp
var uri = new Uri("http://yourOneTrueErrorServer");
OneTrue.Configuration.Credentials(uri, "appKey", "sharedSecret");
```

Once done you can report your first exception using something like this:

```csharp
try
{
    //some stuff that generates an exception
}
catch (Exception ex)
{
    OneTrue.Report(ex);
}
```

The exception should appear in our web moments after you reported it.

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

We also have an object overload which can transform any object into a context collection (one of the groups in the "Context Data" menu in our web site).

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

