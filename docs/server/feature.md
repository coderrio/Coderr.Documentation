Building a new feature
========================

New features should be added in the `codeRR.Api` and `codeRR.App` projects under the "Modules" namespace.

You typically start by adding a new event handler. They are defined like this:

```csharp
[Component(RegisterAsSelf = true)]
public class StorePositionFromNewReport : IApplicationEventSubscriber<ReportAddedToIncident>
{
	public async Task HandleAsync(ReportAddedToIncident e)
	{
	}
}
```

The handler will be picked up and registered in the Inversion Of Control container by the framework. No need to specify a registration somewhere.

The above handler says that it will act upon the events of type `ReportAddedToIncident`. Thus each time a new report is uploaded this handler will be invoked. All
event handlers are run in isolation, if one fails the others will not be aborted. Do note that the same event object will not be retried for the failing handler.

# Creating and implementing an API

If you want to expose an API you define it in the `codeRR.Api` project and then implement the handlers in `codeRR.App`.

For instance you might define a command as `BlockUser` with the following structure:

```csharp
public class BlockUser
{
    public BlockUser(int accountId)
	{
		if (accountId <= 0) throw new ArgumentOutOfRange("accountId");
		AccountId = accountId;
	}
	
    protected BlockUser()
	{
	}
	
	public int AccountId { get; private set; }
}
```

Three design decisions to be aware of:

1. Mandatory fields should be included in the constructor
2. A default constructor must be available for serialization (but is in most cases set to protected)
3. Encapsulation is important in codeRR, use private setters if possible, even on DTOs

Once done you need to implement a handler:

```csharp
[Component(RegisterAsSelf = true)]
public class BlockUserHandler : ICommandHandler<BlockUser>
{
	public async Task ExecuteAsync(BlockUser e)
	{
	    //invoke stuff
	}
}
```

Once done the API need to be exposed to the Web project. To do that run the tool Tools\TsGenerator. It will go through the API projects and update the typescript classes
in the web project.

# Data layer

codeRR uses the repository pattern for the write side, while the query handlers typically uses ADO.NET directly (and is therefore located in the DB projects).

