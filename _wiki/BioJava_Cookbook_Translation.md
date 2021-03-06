---
title: BioJava:Cookbook:Translation
permalink: wiki/BioJava%3ACookbook%3ATranslation
---

How do I translate a DNA or RNA Sequence or SymbolList to Protein?
------------------------------------------------------------------

To translate a DNA sequence you need to do the following

-   [Transcribe to
    RNA](/wiki/BioJava:Cookbook:Sequence:Transcribe "wikilink").
-   Get a triplet (codon) view on the SymbolList.
-   Translate to protein.

Almost all of this can be achieved using static methods from BioJava
tools classes. The following block of code demonstrates the procedure.
Obviously if you already have an RNA sequence there is no need to
transcribe it.

*NOTE: if you try and create a 'triplet view' on a SymbolList or
Sequence who's length is not evenly divisible by three an
IllegalArgumentException will be thrown. See ['how to get a
subsequence'](/wiki/BioJava:Cookbook:Sequence:SubSequence "wikilink") for a
description of how to get a portion of a Sequence for translation.*

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.seq.\*;

public class Translate {

` public static void main(String[] args) {`  
`   try {`  
`     //create a DNA SymbolList`  
`     SymbolList symL = DNATools.createDNA("atggccattgaatga");`

`     //transcribe to RNA (after biojava 1.4 this method is deprecated)`  
`     symL = RNATools.transcribe(symL);`

`     //transcribe to RNA (after biojava 1.4 use this method instead)`  
`     symL = DNATools.toRNA(symL);`  
`     `  
`     //translate to protein`  
`     symL = RNATools.translate(symL);`

`     //prove that it worked`  
`          System.out.println(symL.seqString());`  
`    }catch (IllegalAlphabetException ex) {`  
`     `  
`    `  
`     /* `  
`      * this will occur if you try and transcribe a non DNA sequence or translate`  
`      * a sequence that isn't a triplet view on a RNA sequence.`  
`      */`  
`      ex.printStackTrace();`  
`    }catch (IllegalSymbolException ex) {`  
`     // this will happen if non IUB characters are used to create the DNA SymbolList`  
`      ex.printStackTrace();`  
`    }`  
`  }`

} ```
