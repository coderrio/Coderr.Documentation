Context collections
===================

Context collections is part of the core in Coderr. These collections of telemetry data allows you to quickly and accuratly diagnose errors.
Most of them are automatically generated when Coderr detects a new error. 

## Adding context data

* To manually add context data, read the [reporting](/features/reporting) guide.
* To let Coderr automatically generate custom data, create a [custom context provider](/client/extending/contextprovider/)

## Examples

Hare are a few examples. The integration libraries generate more than these.

### ASP.NET Core MVC


![](/screens/features/context/httprequest.png)

![](/screens/features/context/modelstate.png)

![](/screens/features/context/routedata.png)

### JavaScript

![](/screens/features/context/location.png)

### VueJS

![](/screens/features/context/vuecomponent.png)

