---
title: BioJava:Download 4.2.0
permalink: wiki/BioJava%3ADownload_4.2.0/
---

This page offers downloads for the <b>BioJava 4.2.0 release</b>.

BioJava 4.2.0 is compatible with <b>Java 7 and 8</b>.

About
-----

*BioJava* 4.2.0 has been released and is available using Maven from
Maven Central as well as manual download (see below).

This release contains over
[750 commits](https://github.com/biojava/biojava/compare/6f8d796fee92edbbcd001c33cdae4f15c5480741...biojava-4.2.0)
 from 16 contributors.

### New Features

BioJava 4.2.0 offers many new features, as well several bug-fixes.

General  

-   Requires Java 7
-   Better logging with SLF4J

Biojava-Core  

-   New SearchIO framework including blast xml parser

Biojava-structure  

-   Secondary structure assignment (DSSP compatible)
-   Multiple Structure Alignments
    -   New MultipleStructureAlignment datastructure supporting flexible
        and order-independent alignments
    -   MultipleMC algorithm
        -   Can use any pairwise StructureAlignment implementation
    -   serialize and parse multiple structure alignments as XML files,
        output as Text, FatCat, FASTA, Rotation Matrices, etc.
-   More complete mmCIF and cif parsing
    -   Parse bonds, sites, charges
    -   Better support for non-deposited pdb and mmcif files
-   Include CE-Symm algorithm for finding internal symmetry
    (Myers-Turnbull, 2014)
-   Replaced internal graph datastructures with Jgraph
-   Unified StructureIdentifier framework
-   Improved chemical component framework, now by default providing full
    chemical description by using DownloadChemCompProvider
-   Optimised memory usage of Residue/Atoms

Biojava-structure-gui  

-   MultipleAlignmentGUI for visualizing Multiple Structure Alignments
    with Jmol
-   SymmetryDisplay for visualizing internal symmetry

Biojava-Phylo  

-   Use Forester 1.038
-   Significant bug fixes
-   use SubstitutionMatrices in the core module (instead of imported
    Jalview matrices),
-   use Sequence and Compound classes from the alignment module
-   provide some Wrapper methods to communicate with forester,
-   decouple distance matrix calculation from tree constructor,
-   provide methods for common distance matrix calculations and
    framework for user-defined distances,
-   update the forester version to have the correct NJ tree constructor
    AND
-   correct some of the tree evaluator statistics.

View the <BioJava:Modules> page for a list of current modules.

Maven Download
--------------

BioJava 4.2.0 requires [Maven](http://maven.apache.org/) for the build
process. All BioJava jar files are available via Maven Central as of
this release.

You can create a BioJava dependency by adding the following XML to your
project pom.xml file:

```xml
            <dependencies>
                    <dependency>
                            <groupId>org.biojava</groupId>
                            <artifactId>biojava-core</artifactId>
                            <version>4.2.0</version>
                    </dependency>
                    <!-- other biojava jars as needed -->
            </dependencies> 
```

Manual Download
---------------


| Module                   | Binary Jar                                                                                                                                         | Source Jar                                                                                                                                                         | Javadoc Jar                                                                                                                                                        |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| biojava-core             | [biojava-core-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-core/4.2.0/biojava-core-4.2.0.jar)                                     | [biojava-core-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-core/4.2.0/biojava-core-4.2.0-sources.jar)                                     | [biojava-core-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-core/4.2.0/biojava-core-4.2.0-javadoc.jar)                                     |
| biojava-alignment        | [biojava-alignment-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-alignment/4.2.0/biojava-alignment-4.2.0.jar)                      | [biojava-alignment-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-alignment/4.2.0/biojava-alignment-4.2.0-sources.jar)                      | [biojava-alignment-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-alignment/4.2.0/biojava-alignment-4.2.0-javadoc.jar)                      |
| biojava-genome           | [biojava-genome-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-genome/4.2.0/biojava-genome-4.2.0.jar)                               | [biojava-genome-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-genome/4.2.0/biojava-genome-4.2.0-sources.jar)                               | [biojava-genome-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-genome/4.2.0/biojava-genome-4.2.0-javadoc.jar)                               |
| biojava-structure        | [biojava-structure-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure/4.2.0/biojava-structure-4.2.0.jar)                      | [biojava-structure-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure/4.2.0/biojava-structure-4.2.0-sources.jar)                      | [biojava-structure-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure/4.2.0/biojava-structure-4.2.0-javadoc.jar)                      |
| biojava-structure-gui    | [biojava-structure-gui-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure-gui/4.2.0/biojava-structure-gui-4.2.0.jar)          | [biojava-structure-gui-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure-gui/4.2.0/biojava-structure-gui-4.2.0-sources.jar)          | [biojava-structure-gui-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-structure-gui/4.2.0/biojava-structure-gui-4.2.0-javadoc.jar)          |
| biojava-phylo            | [biojava-phylo-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-phylo/4.2.0/biojava-phylo-4.2.0.jar)                                  | [biojava-phylo-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-phylo/4.2.0/biojava-phylo-4.2.0-sources.jar)                                  | [biojava-phylo-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-phylo/4.2.0/biojava-phylo-4.2.0-javadoc.jar)                                  |
| biojava-modfinder        | [biojava-modfinder-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-modfinder/4.2.0/biojava-modfinder-4.2.0.jar)                      | [biojava-modfinder-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-modfinder/4.2.0/biojava-modfinder-4.2.0-sources.jar)                      | [biojava-modfinder-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-modfinder/4.2.0/biojava-modfinder-4.2.0-javadoc.jar)                      |
| biojava-ws               | [biojava-ws-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ws/4.2.0/biojava-ws-4.2.0.jar)                                           | [biojava-ws-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ws/4.2.0/biojava-ws-4.2.0-sources.jar)                                           | [biojava-ws-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ws/4.2.0/biojava-ws-4.2.0-javadoc.jar)                                           |
| biojava-aa-prop          | [biojava-aa-prop-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-aa-prop/4.2.0/biojava-aa-prop-4.2.0.jar)                            | [biojava-aa-prop-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-aa-prop/4.2.0/biojava-aa-prop-4.2.0-sources.jar)                            | [biojava-aa-prop-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-aa-prop/4.2.0/biojava-aa-prop-4.2.0-javadoc.jar)                            |
| biojava-ontology         | [biojava-ontology-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ontology/4.2.0/biojava-ontology-4.2.0.jar)                         | [biojava-ontology-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ontology/4.2.0/biojava-ontology-4.2.0-sources.jar)                         | [biojava-ontology-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-ontology/4.2.0/biojava-ontology-4.2.0-javadoc.jar)                         |
| biojava-survival         | [biojava-survival-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-survival/4.2.0/biojava-survival-4.2.0.jar)                         | [biojava-survival-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-survival/4.2.0/biojava-survival-4.2.0-sources.jar)                         | [biojava-survival-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-survival/4.2.0/biojava-survival-4.2.0-javadoc.jar)                         |
| biojava-protein-disorder | [biojava-protein-disorder-4.2.0.jar](https://repo1.maven.org/maven2/org/biojava/biojava-protein-disorder/4.2.0/biojava-protein-disorder-4.2.0.jar) | [biojava-protein-disorder-4.2.0-sources.jar](https://repo1.maven.org/maven2/org/biojava/biojava-protein-disorder/4.2.0/biojava-protein-disorder-4.2.0-sources.jar) | [biojava-protein-disorder-4.2.0-javadoc.jar](https://repo1.maven.org/maven2/org/biojava/biojava-protein-disorder/4.2.0/biojava-protein-disorder-4.2.0-javadoc.jar) |

Browse API docs
---------------

You can also browse the documentation at [BioJava 4.2.0
api](http://www.biojava.org/docs/api4.2.0/)

Release Date
------------

BioJava 4.2.0 has been released on March 10th, 2015

Getting older versions
----------------------

-   The release of 4.1.0 can be found
    [here](/wiki/BioJava:Download 4.1.0 "wikilink") (requires Java 1.6, 1.7,
    or 1.8)
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

