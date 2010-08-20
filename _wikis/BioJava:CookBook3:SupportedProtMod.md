---
title: BioJava:CookBook3:SupportedProtMod
---

How can I get the list of supported protein modifications?
----------------------------------------------------------

The protmod module contains[an XML
file](http://code.open-bio.org/svnweb/index.cgi/biojava/browse/biojava-live/trunk/biojava3-protmod/src/main/resources/org/biojava3/protmod),
defining a list of protein modifications, retrieved from [Protein Data
Bank Chemical Component Dictrionary](http://www.wwpdb.org/ccd.html),
[RESID](http://www.ebi.ac.uk/RESID/), and
[PSI-MOD](http://psidev.sourceforge.net/mod/). It contains many common
modifications such glycosylation, phosphorylation, acelytation,
methylation, etc. Crosslinks are also included, such disulfide bonds and
iso-peptide bonds.

The protmod maintains a registry of supported protein modifications. The
list of protein modifications contained in the XML file will be
automatically loaded. You can [ define and add a new protein
modification](AddProtMod "wikilink") if it has not been defined in the
XML file. From the protein modification registry, a user can retrieve

-   all protein modifications,
-   a protein modification by ID,
-   a set of protein modifications by RESID ID,
-   a set of protein modifications by PSI-MOD ID,
-   a set of protein modifications by PDBCC ID,
-   a set of protein modifications by category (attachment, modified
    residue, crosslink1, crosslink2, ..., crosslink7),
-   a set of protein modifications by occurrence type (natural or
    hypothetical),
-   a set of protein modifications by a keyword (glycoprotein,
    phosphoprotein, sulfoprotein, ...),
-   a set of protein modifications by involved components.

Example: retrieve registered protein modifications
--------------------------------------------------

<java> // all protein modifications Set<ProteinModification> mods =
ProteinModification.allModifications();

// a protein modification by ID ProteinModification mod =
ProteinModification.getById("0001");

// a set of protein modifications by RESID ID Set<ProteinModification>
mods = ProteinModification.getByResidId("AA0151");

// a set of protein modifications by PSI-MOD ID Set<ProteinModification>
mods = ProteinModification.getByPsimodId("MOD:00160");

// a set of protein modifications by PDBCC ID Set<ProteinModification>
mods = ProteinModification.getByPdbccId("SEP");

// a set of protein modifications by category Set<ProteinModification>
mods =
ProteinModification.getByCategory(ModificationCategory.ATTACHMENT);

// a set of protein modifications by occurrence type
Set<ProteinModification> mods =
ProteinModification.getByOccurrenceType(ModificationOccurrenceType.NATURAL);

// a set of protein modifications by a keyword Set<ProteinModification>
mods = ProteinModification.getByKeyword("phosphoprotein");

// a set of protein modifications by involved components.
Set<ProteinModification> mods =
ProteinModification.getByComponent(Component.of("FAD",
ComponentType.LIGAND));

</java>