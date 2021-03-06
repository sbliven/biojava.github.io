---
title: BioJava:Cookbook:Translation:Single
permalink: wiki/BioJava%3ACookbook%3ATranslation%3ASingle
---

How do I translate a single codon to a single amino acid?
---------------------------------------------------------

The general translation example shows how to use RNATools to translate a
RNA SymbolList into a Protein SymbolList but most of what goes on is
hidden behind the convenience method translate(). If you only want to
translate a single codon into a single amino acid you get exposed to a
bit more of the gory detail but you also get a chance to figure out more
of what is going on under the hood.

There are actually a number of ways to do this, below I have presented
only one.

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class SingleTranslationDemo {

` public static void main(String[] args) {`  
`   //make a compound alphabet where codons are Symbols`  
`   Alphabet a = AlphabetManager.alphabetForName("(RNA x RNA x RNA)");`

`   //get our translation table using one of the static names from TranslationTable`  
`   TranslationTable table = RNATools.getGeneticCode(TranslationTable.UNIVERSAL);`

`   try {`  
`     //make a 'codon'`  
`     SymbolList codon = RNATools.createRNA("UUG");`

`     //get the representation of that codon as a Symbol`  
`     Symbol sym = a.getSymbol(codon.toList());`

`     //translate to amino acid`  
`     Symbol aminoAcid = table.translate(sym);`  
`     `  
`     /*`  
`      * This bit is not required for the translation it just proves that the`  
`      * Symbol is from the right Alphabet. An Exception will be thrown if it`  
`      * isn't.`  
`      */`  
`     ProteinTools.getTAlphabet().validate(aminoAcid);`

`     //i think it is Leucine`  
`     System.out.println(aminoAcid.getName());`  
`   `  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
