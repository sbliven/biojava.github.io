---
title: BioJava:CookbookFrench:Locations:Filter
permalink: wiki/BioJava%3ACookbookFrench%3ALocations%3AFilter
---

Comment filtrer les Features selon leur type?
---------------------------------------------

Si vous venez de lire un fichier de séquence écrit en format GenBank, le
résultat de cette lecture sera un objet *Sequence* qui contiendra
plusieurs *Features* de types variés. Il est possible que vous ne soyez
interessé que par les *Features* du type "CDS" par exemple. Pour filtrer
les *Features*, vous utiliserez un *FeatureFilter* qui sera utilisé pour
créer un *FeatureHolder* contenant uniquement les *Features* qui sont
passé à travers le *FeatureFilter*.

L'exemple suivant montre l'utilisation d'un *FeatureFilter* "by Type".

```java import java.util.\*;

import org.biojava.bio.seq.\*;

public class FilterByType {

` public static void main(String[] args) {`  
`   Sequence seq = null;`

` /*`  
`  * votre code permettant d'initialiser seq avec une varieté de features`  
`  * possiblement suite à la lecture d'un fichier Genbank ou similaire.`  
`  */`

`   //créer un Filter pour le type "CDS"`  
`   FeatureFilter ff = new FeatureFilter.ByType("CDS");`

`   //obtenir les Features filtres`  
`   FeatureHolder fh = seq.filter(ff);`

`   //itérer sur les Features contenu dans fh`  
`   for (Iterator i = fh.features(); i.hasNext(); ) {`  
`     Feature f = (Feature)i.next();`  
`   }`  
` }`

} ```
