---
title: BioJava:CookBook:PDB:BioJava Algorithm
permalink: wiki/BioJava%3ACookBook%3APDB%3ABioJava_Algorithm
---

This is the example of how to use the structure alignment algorithm with
the BioJava 1.7 release. BioJava \>3 contains an implementation of the
CE and FATCAT algorithms as well.

Biojava 1.7 algorithm
=====================

The [structure alignment
algorithm](/wiki/BioJava:CookBook:PDB:aboutalign "wikilink") contained in
BioJava is based on a variation of the PSC++ algorithm provided by Peter
Lackner, Univ. Salzburg (personal communication). The
[algorithm](/wiki/BioJava:CookBook:PDB:aboutalign "wikilink") is calculating a
distance matrix based, rigid body protein structure superimposition.

Example
-------

[Run WebStart
Example](http://www.biojava.org/download/performance/biojava-structure-example1.jnlp)
(5MB download includes Jmol for visualization)

Learn more about this JavaWebStart example at <BioJava:Performance>

Code
----

```java

` public static void main(String[] args){`

`       PDBFileReader pdbr = new PDBFileReader();`  
`       pdbr.setPath("/Path/To/My/PDBFiles/");`

`       String pdb1 = "1buz";`  
`       String pdb2 = "1ali";`  
`       String outputfile = "/somewhere/alig_" + pdb1 + "_" + pdb2 + ".pdb";`

`       try {`  
`           // NO NEED TO DO CHANGE ANYTHING BELOW HERE...`

`           StructurePairAligner sc = new StructurePairAligner();`

`           // step1 : read molecules`

`           System.out.println("aligning " + pdb1 + " vs. " + pdb2);`

`           Structure s1 = pdbr.getStructureById(pdb1);`  
`           Structure s2 = pdbr.getStructureById(pdb2);`  
`           // of course you do not have to use the full structures`  
`           // you could also just use any set of atoms of your choice`

`           // step 2 : do the calculations`  
`           sc.align(s1, s2);`

`           // if you want more control over the alignment parameters`  
`           // use the StrucAligParameters`  
`           // StrucAligParameters params = new StrucAligParameters();`  
`           // params.setFragmentLength(8);`  
`           // sc.align(s1,s2,params);`

`           AlternativeAlignment[] aligs = sc.getAlignments();`

`           // cluster similar results together`  
`           ClusterAltAligs.cluster(aligs);`

`           // print the result:`  
`           // the AlternativeAlignment object gives access to rotation matrices`  
`           // / shift vectors.`  
`           for (int i = 0; i < aligs.length; i++) {`  
`               AlternativeAlignment aa = aligs[i];`  
`               System.out.println(aa);`  
`           }`

`           // convert AlternativeAlignment 1 to PDB file, so it can be opened`  
`           // with a viewer of your choice`  
`           // (e.g. Jmol, Rasmol)`

`           if (aligs.length > 0) {`  
`               AlternativeAlignment aa1 = aligs[0];`  
`               String pdbstr = aa1.toPDB(s1, s2);`

`               System.out.println("writing alignment to " + outputfile);`  
`               FileOutputStream out = new FileOutputStream(outputfile);`  
`               PrintStream p = new PrintStream(out);`

`               p.println(pdbstr);`

`               p.close();`  
`               out.close();`  
`           }`  
`       } catch (FileNotFoundException e) {`  
`           // TODO Auto-generated catch block`  
`           e.printStackTrace();`  
`       } catch (IOException e) {`  
`           // TODO Auto-generated catch block`  
`           e.printStackTrace();`  
`       } catch (StructureException e) {`  
`           e.printStackTrace();`  
`       }`

} ```

You can send the structure alignment for display to Jmol. see
<BioJava:CookBook:PDB:Jmol> for more on this.
