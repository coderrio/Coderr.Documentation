
OneTrueError.Client installation
=================================

You've just installed the OneTrueError client. 

To get started add the following code to your application:

```csharp
var url = new Uri("http://yourServer/onetrueerror/");
OneTrue.Configuration.Credentials(url, "yourAppKey", "yourSharedSecret");
```

Once done you can report exceptions like this:

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


## More information

* [Client library](../index.md)
* [Server guide (to modify the server source code)](../../server.md)


*(this library requires that you have installed a OneTrueError server somewhere)*
