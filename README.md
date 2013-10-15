About
-----
The Junit XML Listener is a simple sbt test listener plugin that collects the results of test runs and writes them to an xml file formatted like the output of a JUnit run.
This allows the test results to be displayed in any tool that can display JUnit results (e.g. Jenkins)

Known Issues
------------
The time for each test group run is set to 0s as there are no ways I know of to measure that time.


Requirements
------------

* sbt 0.13.0

Installation
------------

Add the following lines to either ~/.sbt/plugins/build.sbt (user-specific) or project/plugins/build.sbt (project-specific):

    //You need to add the resolver as long as the plugin is only published to the snapshots repo. 
    //As soon as it is in central, you can remove this additional resolver.
    resolvers += "Scala Snapshots" at "https://oss.sonatype.org/content/repositories/snapshots/"

    addSbtPlugin("eu.henkelmann" % "junit_xml_listener" % "0.4-SNAPSHOT")

This will add the dependency to the plugin. The next step is to configure your build to output the XML. The following will output the XML in target/{scala-version}/test-reports:

    testListeners := Seq(new eu.henkelmann.sbt.JUnitXmlTestsListener(crossTarget.value.getAbsolutePath))

Note that the line as shown is enough in a *.sbt file. In *.scala files (full configuration), you must collect the result of the expression into the settings of all projects that should produce the XML output.

Version History
---------------

* 0.4-SNAPSHOT first version published to maven central (snapshots)
* 0.3 Merge of Ismael Juma's adjustments for sbt 0.10+
* 0.2 Added handling of skipped tests (thanks to Johannes Rudolph)
* 0.1 Initial release
