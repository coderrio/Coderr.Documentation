OneTrueError documentation
===============

This documentation is divided into two sections:

* [Client documentation](client/index.md)
* [Server documentation](server/index.md)

# OneTrueError pipeline

Below is an illustration that shows the OneTrueError pipeline, from detecting the exception to analyzing it in the server.
Do note that all analysis services typically subscribe on the `ReportAddedToIncident` event, thus all analysers will be invoked
when the pipeline shown in the image ends.

![](pipeline.png)
