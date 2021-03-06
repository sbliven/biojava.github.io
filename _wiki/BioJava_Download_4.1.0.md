---
title: BioJava:Download 4.1.0
permalink: wiki/BioJava%3ADownload_4.1.0/
---

This page offers downloads for the <b>BioJava 4.1.0 release</b>.

BioJava 4.1.0 is compatible with <b>Java 6, 7, and 8</b>.

About
-----

*BioJava* 4.1.0 has been released and is available using Maven from
Maven Central as well as manual download (see below).

This release contains over
[<https://github.com/biojava/biojava/compare/5131f3aaff5a5bbbf221f5f52cfe3b849a002d87>...biojava-4.1.0
240] commits from 8 contributors.

### New Features

BioJava 4.1.0 offers a few new features, as well several bug-fixes.

New Features:

-   New algorithm for multiple structure alignments
-   Improved visualization of structural alignments in Jmol
-   Support for the ECOD protein classification
-   Better mmCIF support: limited write support, better parsing

View the <BioJava:Modules> page for a list of current modules.

Maven Download
--------------

BioJava 4.1.0 requires [Maven](http://maven.apache.org/) for the build
process. All BioJava jar files are available via Maven Central as of
this release.

You can create a BioJava dependency by adding the following XML to your
project pom.xml file:

            <dependencies>
                    <dependency>
                            <groupId>org.biojava</groupId>
                            <artifactId>biojava-core</artifactId>
                            <version>4.1.0</version>
                    </dependency>
                    <!-- other biojava jars as needed -->
            </dependencies> 

Manual Download
---------------

.tar.gz containing all jars, source and javadocs:
[biojava-4.1.0-all](http://biojava.org/download/bj4.1.0/biojava-4.1.0-all.tar.gz)

| Module                   | Binary Jar                                                                                                                                         | Source Jar                                                                                                                                                         | Javadoc Jar                                                                                                                                                        |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| biojava-core             | [biojava-core-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-core/4.1.0/biojava-core-4.1.0.jar)                                     | [biojava-core-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-core/4.1.0/biojava-core-4.1.0-sources.jar)                                     | [biojava-core-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-core/4.1.0/biojava-core-4.1.0-javadoc.jar)                                     |
| biojava-alignment        | [biojava-alignment-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-alignment/4.1.0/biojava-alignment-4.1.0.jar)                      | [biojava-alignment-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-alignment/4.1.0/biojava-alignment-4.1.0-sources.jar)                      | [biojava-alignment-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-alignment/4.1.0/biojava-alignment-4.1.0-javadoc.jar)                      |
| biojava-genome           | [biojava-genome-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-genome/4.1.0/biojava-genome-4.1.0.jar)                               | [biojava-genome-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-genome/4.1.0/biojava-genome-4.1.0-sources.jar)                               | [biojava-genome-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-genome/4.1.0/biojava-genome-4.1.0-javadoc.jar)                               |
| biojava-structure        | [biojava-structure-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure/4.1.0/biojava-structure-4.1.0.jar)                      | [biojava-structure-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure/4.1.0/biojava-structure-4.1.0-sources.jar)                      | [biojava-structure-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure/4.1.0/biojava-structure-4.1.0-javadoc.jar)                      |
| biojava-structure-gui    | [biojava-structure-gui-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure-gui/4.1.0/biojava-structure-gui-4.1.0.jar)          | [biojava-structure-gui-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure-gui/4.1.0/biojava-structure-gui-4.1.0-sources.jar)          | [biojava-structure-gui-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure-gui/4.1.0/biojava-structure-gui-4.1.0-javadoc.jar)          |
| biojava-phylo            | [biojava-phylo-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-phylo/4.1.0/biojava-phylo-4.1.0.jar)                                  | [biojava-phylo-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-phylo/4.1.0/biojava-phylo-4.1.0-sources.jar)                                  | [biojava-phylo-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-phylo/4.1.0/biojava-phylo-4.1.0-javadoc.jar)                                  |
| biojava-modfinder        | [biojava-modfinder-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-modfinder/4.1.0/biojava-modfinder-4.1.0.jar)                      | [biojava-modfinder-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-modfinder/4.1.0/biojava-modfinder-4.1.0-sources.jar)                      | [biojava-modfinder-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-modfinder/4.1.0/biojava-modfinder-4.1.0-javadoc.jar)                      |
| biojava-ws               | [biojava-ws-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ws/4.1.0/biojava-ws-4.1.0.jar)                                           | [biojava-ws-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ws/4.1.0/biojava-ws-4.1.0-sources.jar)                                           | [biojava-ws-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ws/4.1.0/biojava-ws-4.1.0-javadoc.jar)                                           |
| biojava-aa-prop          | [biojava-aa-prop-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-aa-prop/4.1.0/biojava-aa-prop-4.1.0.jar)                            | [biojava-aa-prop-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-aa-prop/4.1.0/biojava-aa-prop-4.1.0-sources.jar)                            | [biojava-aa-prop-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-aa-prop/4.1.0/biojava-aa-prop-4.1.0-javadoc.jar)                            |
| biojava-ontology         | [biojava-ontology-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ontology/4.1.0/biojava-ontology-4.1.0.jar)                         | [biojava-ontology-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ontology/4.1.0/biojava-ontology-4.1.0-sources.jar)                         | [biojava-ontology-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ontology/4.1.0/biojava-ontology-4.1.0-javadoc.jar)                         |
| biojava-survival         | [biojava-survival-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-survival/4.1.0/biojava-survival-4.1.0.jar)                         | [biojava-survival-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-survival/4.1.0/biojava-survival-4.1.0-sources.jar)                         | [biojava-survival-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-survival/4.1.0/biojava-survival-4.1.0-javadoc.jar)                         |
| biojava-protein-disorder | [biojava-protein-disorder-4.1.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-protein-disorder/4.1.0/biojava-protein-disorder-4.1.0.jar) | [biojava-protein-disorder-4.1.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-protein-disorder/4.1.0/biojava-protein-disorder-4.1.0-sources.jar) | [biojava-protein-disorder-4.1.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-protein-disorder/4.1.0/biojava-protein-disorder-4.1.0-javadoc.jar) |

Browse API docs
---------------

You can also browse the documentation at [BioJava 4.1.0
api](http://www.biojava.org/docs/api4.1.0/)

Release Date
------------

BioJava 4.1.0 has been released on June 25th, 2015

Getting older versions
----------------------

-   The release of 4.0.0 can be found
    [here](/wiki/BioJava:Download 4.0.0 "wikilink") (requires Java 1.6, 1.7,
    or 1.8)
-   The release of 3.1.0 can be found
    [here](/wiki/BioJava:Download 3.1.0 "wikilink") (requires Java 1.6 or 1.7)
-   The release of 3.0.8 can be found
    [here](/wiki/BioJava:Download 3.0.8 "wikilink") (requires Java 1.6+)
-   The release of 3.0.7 can be found
    [here](/wiki/BioJava:Download 3.0.7 "wikilink") (requires Java 1.6+)
-   The release of 3.0.6 can be found
    [here](/wiki/BioJava:Download 3.0.6 "wikilink") (requires Java 1.6+)
-   The release of 3.0.5 can be found
    [here](/wiki/BioJava:Download 3.0.5 "wikilink") (requires Java 1.6+)
-   The release of 3.0.4 can be found
    [here](/wiki/BioJava:Download 3.0.4 "wikilink") (requires Java 1.6+)
-   The release of 3.0.3 can be found
    [here](/wiki/BioJava:Download 3.0.3 "wikilink") (requires Java 1.6+)
-   The release of 3.0.2 can be found
    [here](/wiki/BioJava:Download 3.0.2 "wikilink") (requires Java 1.6+)
-   The release of 3.0.1 can be found
    [here](/wiki/BioJava:Download 3.0.1 "wikilink") (requires Java 1.6+)
-   The release of 3.0 can be found
    [here](/wiki/BioJava:Download 3.0 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.9.1 can be found
    [here](/wiki/BioJava:Download 1.9.1 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.9.0 can be found
    [here](/wiki/BioJava:Download 1.9.0 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.8.5 can be found
    [here](/wiki/BioJava:Download 1.8.5 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.8.4 can be found
    [here](/wiki/BioJava:Download 1.8.4 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.8.2 can be found
    [here](/wiki/BioJava:Download 1.8.2 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.8.1 can be found
    [here](/wiki/BioJava:Download 1.8.1 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.7.1 can be found
    [here](/wiki/BioJava:Download 1.7.1 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.7 can be found
    [here](/wiki/BioJava:Download 1.7 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.6 can be found
    [here](/wiki/BioJava:Download 1.6 "wikilink") (requires Java 1.5+)
-   The legacy release of 1.5 can be found
    [here](/wiki/BioJava:Download 1.5 "wikilink") (requires Java 1.4.2+)
-   The legacy release of 1.4 can be found
    [here](/wiki/BioJava:Download 1.4 "wikilink")
-   The legacy release 1.3 can be found
    [here](/wiki/BioJava:Download 1.3 "wikilink").
-   Older releases of BioJava can be found in the [download
    area](http://www.biojava.org/download/).

