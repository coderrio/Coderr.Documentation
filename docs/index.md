OneTrueError documentation
===============

The documentation is divided into two sections.
Both sections contains information about how you can contribute to OneTrueError and how you can adapt/integrate with OTE.

# Client documentation

Information about how you can download, configure and use OneTrueError within our application.

[Client documentation](client/index.md)

# Server documentation

Information about how you can install and configure the server that receives and analyses all error reports.

[Server documentation](server/index.md)

# OneTrueError pipeline

Below is an illustration that shows the OneTrueError pipeline, from detecting the exception to analyzing it in the server.
Do note that all analysis services typically subscribe on the `ReportAddedToIncident` event, thus all analysers will be invoked
when the pipeline shown in the image ends.

![](pipeline.png)
