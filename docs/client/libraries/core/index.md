.NET 4.x - Core library information
=================================

This library is the foundation of all exception reporting done with Coderr. All other client libraries are based upon this one.

To get help installing it, [read here](install.md).

## Context collections

There are  few built in context collections in the core library. Some are added to the pipeline per default while others require you to add them manually.

### Application information

This collection includes information about your process. It contains information like used memory, thread count and ...

![](collections/applicationinfo.png)

### Assemblies

All assemblies that have been loaded into the AppDomain.

![](collections/assemblies.png)

### Exception information

Information from the exception, including all properties.

![](collections/exception.png)

### File versions

File versions for all assemblies, as the assembly version might be the same while the file version is higher.

![](collections/fileversions.png)

### Operating system

Operating system information

![](collections/operatingsystem.png)

### System information

System information

![](collections/systeminfo.png)

### Thread information

Thread information like specified UI culture.

![](collections/thread.png)

## More information

* [Client API reference](https://coderr.io/docs/api/client/)
* [Getting started guide](../../gettingstarted.md)
