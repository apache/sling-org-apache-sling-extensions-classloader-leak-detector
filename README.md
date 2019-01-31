[<img src="https://sling.apache.org/res/logos/sling.png"/>](https://sling.apache.org)

 [![Build Status](https://builds.apache.org/buildStatus/icon?job=Sling/sling-org-apache-sling-extensions-classloader-leak-detector/master)](https://builds.apache.org/job/Sling/job/sling-org-apache-sling-extensions-classloader-leak-detector/job/master) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.apache.sling/org.apache.sling.extensions.classloader-leak-detector/badge.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.apache.sling%22%20a%3A%22org.apache.sling.extensions.classloader-leak-detector%22) [![JavaDocs](https://www.javadoc.io/badge/org.apache.sling/org.apache.sling.extensions.classloader-leak-detector.svg)](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.extensions.classloader-leak-detector) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

# Apache Sling ClassLoader Leak Detector

This module is part of the [Apache Sling](https://sling.apache.org) project.

This bundle provides support for tracing classloader leaks which occur due to
improper cleanup in bundles. Refer to [SLING-3359][1] for background details.

The bundle registers a Felix Configuration Printer which dumps out a list of
suspected classloaders which are not getting garbage collected.
It can be accessed at http://localhost:8080/system/console/status-leakdetector

    Possible classloader leak detected
    Number of suspicious bundles - 1

    * org.apache.sling.sample.leakdetector.bad-bundle (0.0.1.SNAPSHOT) - Classloader Count [2]
         - Bundle Id - 204
         - Leaked classloaders
             - Identity HashCode - 4a273519, Creation time 31.01.2014 15:22:58.407

### JVM Arguments

 By default on Oracle JDK the classloaders and related classes from Permgen are
 not garbage collected by default. This bundle relies on classloaders getting
 garbage collected for it work. So to enable that pass on following arguments

     -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled

[1]: https://issues.apache.org/jira/browse/SLING-3359
