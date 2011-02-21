---
title: BioJava talk:CookBook3:NCBIQBlastService
---

Converted entry.getValue() to string before submitting it to
sendAlignmentRequest because it won't catch the DNASequence version.

Also, it keeps giving this error due to a bug in the biojava code:
java.lang.Exception: *The key named PROGRAM is not set in this
RemoteQBlastOutputProperties object*

------------------------------------------------------------------------

Hi,

Thanks for the input. I'll look into this ASAP.

--[Foisys](User:Foisys "wikilink") 12:41, 19 February 2011 (UTC)

------------------------------------------------------------------------

HI,

Ok, here goes:

Your first bug might be related to the fact that in my example code, you
read a file with ProteinSequences in an array and ProteinSequence
objects are what is expected here:

<java>

`           for (Entry`<String, ProteinSequence>` entry : a.entrySet()) {`  
`               System.out.println( entry.getValue().getOriginalHeader() + "\n");`  
`               request = rbw.sendAlignmentRequest(entry.getValue(),rqb);`  
`               rid.add(request);           }`

</java>

If you are using DNASequences, you need to do this:

<java> for (Entry<String, DNASequence> entry : a.entrySet()) {

`               System.out.println( entry.getValue().getOriginalHeader() + "\n");`  
`               request = rbw.sendAlignmentRequest(entry.getValue(),rqb);`  
`               rid.add(request);           }`

</java>

I can tell you this works a-ok :-)

The second thing is a bug in the code that I have now fixed in the
biojava-live svn. Please give it a try and let me know if it works. It
does for me...

--[Foisys](User:Foisys "wikilink") 01:45, 21 February 2011 (UTC)