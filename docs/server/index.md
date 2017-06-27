Server development
======================

This section is dedicated to server development with focus on how new features can be implemented.

* [Server API](http://onetrueerror.com/docs/api/server)
* [Installation guide](installation.md)

# Core concepts

The server is based on CQRS, with the exception that the read/write models have not yet been separated two own databases. 

Events drive changes in different parts of the system. Each namespace in the App/Core and App/Modules root namespaces should be considered to be
isolated domains. They may NOT use functionality from other domains by using anything else than the public CQRS API (i.e. Commands/Queries/Events).

Although the test coverage is poor today, the goal is to improve coverage in all future development. All new features should also be covered by tests.
Thus all classes must be testable
which means that dependencies should be injected. All classes should in most cases also depend on abstractions and not concrete implementations.
Tests should be written to prove that the code fulfil the functional requirements (and not to prove that the code works as it was originally written). Thus
avoid test names like `Get_Null_ThrowException`, use names focusing_on_functionality like `UserId_is_required_to_be_able_to_load_a_user`. 

Modules should be as independent as possible, thus it's better if you store information in the module tables from other modules events rather than 
querying the other modules for information.

The goal is that the entire OneTrueError server should be asynchronous, i.e. using `async`/`await` everywhere. That goal is almost fully achieved, there are
however some issues here and there. All new code should however be asynchronous.

Finally everything should be documented using XmlDoc. The documentation should not mirror the class/method naming but instead try to put classes/methods into
context and explain what the purpose of the class/method is. 

Pull requests will be rejected if the above items have not been included.

# Implementation tutorials

* [Building a new feature](feature.md)
* [Adding support for a new database engine](dbengine.md)
