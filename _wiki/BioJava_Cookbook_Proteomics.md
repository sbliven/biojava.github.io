---
title: BioJava:Cookbook:Proteomics
permalink: wiki/BioJava%3ACookbook%3AProteomics
---

How can I calculate the mass and pI of a peptide?
-------------------------------------------------

If you are doing a proteomics project it is important to know what the
approximate mass and pI of any putative gene is. BioJava contains two
classes (MassCalc and IsoelectricPointCalc) from its proteomics package
that will calculate these numbers for you.

The program below demonstrates a basic usage of these classes. This
simple example uses fairly default settings but both MassCalc and
IsoelectricPointCalc have other specialised options that are not
demosntrated here. Consult the biojava API docs for these options.

```java import java.io.BufferedReader; import java.io.FileOutputStream;
import java.io.FileReader; import java.io.PrintWriter;

import org.biojava.bio.BioException; import
org.biojava.bio.proteomics.IsoelectricPointCalc; import
org.biojava.bio.proteomics.MassCalc; import
org.biojava.bio.seq.ProteinTools; import org.biojava.bio.seq.RNATools;
import org.biojava.bio.seq.Sequence; import
org.biojava.bio.seq.SequenceIterator; import
org.biojava.bio.seq.io.SeqIOTools; import org.biojava.bio.symbol.Edit;
import org.biojava.bio.symbol.IllegalAlphabetException; import
org.biojava.bio.symbol.IllegalSymbolException; import
org.biojava.bio.symbol.SimpleSymbolList; import
org.biojava.bio.symbol.SymbolList; import
org.biojava.bio.symbol.SymbolPropertyTable;

/\*\*

`* Calculates the mass and Isoelectric point of a collection of`  
`* sequences  `  
`*/`

public class CalcMass {

` /**`  
`  * Call this to get usage info, program terminates after call.`  
`  */`  
` public static void help(){`  
`   System.out.println(`  
`       "usage: java calcMass `<file>` `<format>` `<DNA|RNA|PROTEIN>` `<out file>`");`  
`   System.exit( -1);`

` }`

` public CalcMass() {`  
` }`

` /**`  
`  * Calculates the Mass of the peptide in Daltons. Using the average Isotope`  
`  * Mass`  
`  * @param protein the peptide`  
`  * @throws IllegalSymbolException if ``protein`` is not a protein`  
`  * @return the mass`  
`  */`  
` public double mass(SymbolList protein)throws IllegalSymbolException{`  
`   double mass = 0.0;`  
`   MassCalc mc = new MassCalc(SymbolPropertyTable.AVG_MASS, true);`  
`   mass = mc.getMass(protein);`  
`   return mass;`  
` }`

` /**`  
`  * Calculates the isoelectric point assuming a free NH and COOH`  
`  * @param protein the peptide`  
`  * @throws IllegalAlphabetException if ``protein`` is not a peptide`  
`  * @throws BioException`  
`  * @return double the PI`  
`  */`  
` public double pI(SymbolList protein)`  
`     throws IllegalAlphabetException, BioException{`

`   double pI = 0.0;`  
`   IsoelectricPointCalc ic = new IsoelectricPointCalc();`  
`   pI = ic.getPI(protein, true, true);`  
`   return pI;`  
` }`

` public static void main(String[] args) throws Exception{`  
`   if(args.length != 4)`  
`     help();`

`   BufferedReader br = null;`  
`   PrintWriter out = null;`  
`   try{`  
`     //read sequences`  
`     br = new BufferedReader(new FileReader(args[0]));`  
`     SequenceIterator seqi =`  
`         (SequenceIterator)SeqIOTools.fileToBiojava(args[1], args[2], br);`

`     out = new PrintWriter(new FileOutputStream(args[3]));`

`     //write header`  
`     out.println("name, mass, pI, size, sequence");`

`     //initialize calulator`  
`     CalcMass calcMass = new CalcMass();`

`     while (seqi.hasNext()) {`  
`       SymbolList syms = seqi.nextSequence();`  
`       String name = null;`

`       //get an appropriate name for the peptide`  
`       if(args[1].equalsIgnoreCase("fasta")){`  
`         name = ((Sequence) syms).getAnnotation().`  
`             getProperty("description_line").toString();`  
`       }else{`  
`         name = ((Sequence)syms).getName();`  
`       }`  
`       out.print(name+",");`

`       //if not protein we need to translate it.`  
`       if(syms.getAlphabet() != ProteinTools.getAlphabet() &&`  
`          syms.getAlphabet() != ProteinTools.getTAlphabet()){`  
`         if(syms.getAlphabet() != RNATools.getRNA()){`  
`           syms = RNATools.transcribe(syms);`  
`         }`

`         //if not divisible by three truncate`  
`         if(syms.length() % 3 != 0){`  
`           syms = syms.subList(1, syms.length() - (syms.length() %3));`  
`         }`

`         syms = RNATools.translate(syms);`

`        /*`  
`         * Translation of GTG or TTG actually results in a Methionine if`  
`         * it is the start codon (all proteins start with f-Met). Therefore`  
`         * we need to edit the sequence.`  
`         */      `  
`         if(syms.symbolAt(1) != ProteinTools.met()){`  
`           `  
`           //SimpleSymbolLists are editable others may not be`  
`           syms = new SimpleSymbolList(syms);`  
`           Edit e = new Edit(1, syms.getAlphabet(), ProteinTools.met());`  
`           syms.edit(e);`  
`         }`  
`       }`

`       //if the seq ends with a * (termination) we need to remove the *`  
`       if (syms.symbolAt(syms.length()) == ProteinTools.ter()) {`  
`         syms = syms.subList(1, syms.length()-1);`  
`       }`

`       //do calculations`  
`       double mass = calcMass.mass(syms);`  
`       double pI = calcMass.pI(syms);`

`       //print result for this protein`  
`       out.println(mass+","+pI+","+syms.length()+","+syms.seqString());`  
`     }`  
`   }`  
`   finally{ //tidy up`  
`     if(br != null){`  
`       br.close();`  
`     }`  
`     if(out != null){`  
`       out.flush();`  
`       out.close();`  
`     }`  
`   }`  
` }`

} ```
