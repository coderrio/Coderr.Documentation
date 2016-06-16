Client library
===============

Client libraries typically inject themselves into the exception pipeline of a framework. For instance the ASP.NET package uses the `Application.OnError` method while the ASP.NET MVC library uses an exception filter.

# Configuration

The convention is that you create an extension method for the `OneTrueConfiguration` class and name it like `Catch[LibraryName]Exceptions()`. 

Example from the ASP.NET MVC5 extension:

```csharp
// Note that it's in the base library's namespace (for intellisense discovery)
namespace OneTrueError.Client
{
    public static class ConfigurationExtensions
    {
        public static void CatchMvcExceptions(this OneTrueConfiguration configurator)
        {
			// add the custom context collectors
			// provided for the framework that you support
            configurator.ContextProviders.Add(new FormProvider());
            configurator.ContextProviders.Add(new QueryStringProvider());
            configurator.ContextProviders.Add(new SessionProvider());
            configurator.ContextProviders.Add(new HttpHeadersProvider());
			
			// framework extension activation
            GlobalFilters.Filters.Add(new OneTrueErrorFilter());
            ErrorHttpModule.Activate();
        }
    }
}
```

# Custom context collector

All you need to do is to implement `IContextInfoProvider` (and register the collector as shown above):

Example from the ASP.NET MVC5 extension:

```csharp
public class SessionProvider : IContextInfoProvider
{
	public ContextCollectionDTO Collect(IErrorReporterContext context)
	{
		if (HttpContext.Current.Session == null)
			return new ContextCollectionDTO("HttpSession", new NameValueCollection());

		var items = new NameValueCollection();
		foreach (string key in HttpContext.Current.Session)
		{
			var item = HttpContext.Current.Session[key];
			if (item is string)
				items.Add(key, (string) item);
			else
			{
				var json = JsonConvert.SerializeObject(item);
				items.Add(key, json);
			}
		}

		return new ContextCollectionDTO("HttpSession", items);
	}

	public string Name
	{
		get { return "HttpSession"; }
	}
}
```

# Starting the collection pipeline

When an exception is discovered you need to start the collection pipeline. That's done in the same way as reporting exceptions manually (by invoking `OneTrue.Report()`). 

There are however a special overload which can be useful for extension libraries. And that's this one: `ErrorReportDTO GenerateReport(IErrorReporterContext context)`. The context is passed to all context info providers and you can therefore create your custom implementation of it to allow your context collectors to get additional information during the collection process.

Something like:

```csharp
public class AspNetContext : IErrorReporterContext
{
	public AspNetContext(object reporter, Exception exception, HttpContextBase httpContext)
	{
		if (reporter == null) throw new ArgumentNullException("reporter");
		if (exception == null) throw new ArgumentNullException("exception");
		Exception = exception;
		HttpContext = httpContext;
		Reporter = reporter;
	}

	public HttpContextBase HttpContext { get; private set; }

	public Exception Exception { get; private set; }

	public object Reporter { get; private set; }
}
```

The important thing to remember is that the custom context is only included when `OneTrue.GenerateReport` is invoked from your extension point. When exceptions are manually reported it's typically not used. Thus make sure that you can handle that in your context providers.

