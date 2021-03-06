---
title: BioJava:CookbookFrench:Annotations:Filter
permalink: wiki/BioJava%3ACookbookFrench%3AAnnotations%3AFilter
---

Comment filtrer les séquences selon leur espèce d'origine?
----------------------------------------------------------

Le champ "espèce" (ou autre) d'une séquence en format GenBank, SwissProt
ou EMBL aboutit dans une entrée de type Annotation. Tout ce qu'il y a à
faire essentiellement est d'obtenir la propriété de l'espèce des
annotations de chaque séquence et de vérifier celle que l'on veut.

La propriété de l'espèce dépends du fichier source: pour EMBL et
SwissProt, c'est "OS", pour GenBank, c'est "Organism".

Le programme suivant va lire les sequences d'un fichier et les filtrer
selon l'espèce. La même recette de base peut être utilisé, avec quelques
modifications, pour rechercher n'importe quelle propriété d'une
*Annotation*.

```java import java.io.\*;

import org.biojava.bio.\*; import org.biojava.bio.seq.\*; import
org.biojava.bio.seq.db.\*; import org.biojava.bio.seq.io.\*;

public class FilterEMBLBySpecies {

` public static void main(String[] args) {`  
`  try {`  
`     //lire un fichier  EMBL  specifié en args[0]`  
`     BufferedReader br = new BufferedReader(new FileReader(args[0]));`  
`     SequenceIterator iter = SeqIOTools.readEmbl(br);`

`     //le nom de l'espèce à chercher (spécifié par args[1]);`  
`     String species = args[1];`

`     //une SequenceDB pour stocker les Sequences filtrées`  
`     SequenceDB db = new HashSequenceDB();`

`     //lorsque chaque séquence est lue`  
`     while(iter.hasNext()){`  
`       Sequence seq = iter.nextSequence();`  
`       Annotation anno = seq.getAnnotation();`

`       //vérifier si l'Annotation contient le champs "OS"`  
`       if(anno.containsProperty("OS")){`

`         String property = (String)anno.getProperty("OS");`

`         //vérifier la valeur de la proprieté; pourrait être une expression régulière`  
`         if(property.startsWith(species)){`  
`           db.addSequence(seq);`  
`         }`  
`       }`  
`     }`  
`     //écrire les séquences en format FASTA`  
`     SeqIOTools.writeFasta(System.out, db);`  
`   }`  
`  catch (Exception ex) {`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
