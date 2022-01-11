[![Apache Sling](https://sling.apache.org/res/logos/sling.png)](https://sling.apache.org)

&#32;[![Build Status](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-extensions-classloader-leak-detector/job/master/badge/icon)](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-extensions-classloader-leak-detector/job/master/)&#32;[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=apache_sling-org-apache-sling-extensions-classloader-leak-detector&metric=coverage)](https://sonarcloud.io/dashboard?id=apache_sling-org-apache-sling-extensions-classloader-leak-detector)&#32;[![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=apache_sling-org-apache-sling-extensions-classloader-leak-detector&metric=alert_status)](https://sonarcloud.io/dashboard?id=apache_sling-org-apache-sling-extensions-classloader-leak-detector)&#32;[![JavaDoc](https://www.javadoc.io/badge/org.apache.sling/org.apache.sling.extensions.classloader-leak-detector.svg)](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.extensions.classloader-leak-detector)&#32;[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.apache.sling/org.apache.sling.extensions.classloader-leak-detector/badge.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.apache.sling%22%20a%3A%22org.apache.sling.extensions.classloader-leak-detector%22)&#32;[![Contrib](https://sling.apache.org/badges/status-contrib.svg)](https://github.com/apache/sling-aggregator/blob/master/docs/status/contrib.md) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

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
