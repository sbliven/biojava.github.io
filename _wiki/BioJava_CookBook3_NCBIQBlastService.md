---
title: BioJava:CookBook3:NCBIQBlastService
permalink: wiki/BioJava%3ACookBook3%3ANCBIQBlastService
---

How can I use NCBIQBlastService to do my alignments remotely?
-------------------------------------------------------------

BioJava now has some ability to use remote bioinformatics services to
execute tasks on servers and fetch the results for further use. The
first example of this new ability is the capacity to perform Blast
analysis via the Blast URLAPI (formerly known as QBlast) service at
NCBI. Not strictly speaking a web service in the true sense of the word,
Blast URLAPI protocol uses specially formatted HTTP requests to execute
Blast searches on NCBI servers.

The QBlast BioJava classes implement a serie of interfaces:
RemotePairwiseAlignmentService, RemotePairwiseAlignmentProperties and
RemotePairwiseAlignmentOutputProperties. These interfaces are designed
in such a fashion that setting the parameters for alignement, submitting
the results and fetching the results in a desired format are done
independently from each other. This allows a program to send a bunch of
requests, grab the requests ID and fetch the results at a later time.
These interfaces (found in package org.biojava3.ws.alignment) should
allow extensions to other remote alignment services like FASTA and Blast
at EBI, which use classic web services.

To use Blast via URLAPI, use a NCBIQBlastService object (which
implements RemotePairwiseAlignmentService) to manage the connection to
the NCBI Blast service, submission of requests and fetching of results.
To send Blast request to NCBI servers, it needs a sequence (represented
by either a string or a Sequence object) or GID and a
NCBIQBlastAlignmentProperties object. Submitting a Sequence object is
the preferred method since it allows for some basic sanity checks
related to the sequence type-to-program selection. The
NCBIQBlastAlignmentProperties class (which implements
RemotePairwiseAlignmentProperties) is used to set search request
parameters. Most often used parameters have wrapper methods, e.g.
setBlastProgram(BlastProgramEnum program), other options should be set
using setAlignmentOption(BlastAlignmentParameterEnum, String) method.
After sending the request NCBIQBlastService returns request ID (RID),
which is used to fetch the results later. To recover Blast results later
simply pass RID along with NCBIQBlastOutputProperties object to
NCBIQBlastService. Similarly to alignment options, output parameters are
set by using NCBIQBlastOutputProperties wrapper methods or its
setOutputOption(BlastOutputParameterEnum, String) method.

Description of Blast URLAPI and its parameters can be found at
[1](http://www.ncbi.nlm.nih.gov/staff/tao/URLAPI/new/index.html).

**WARNING (as of February 2012):**

- You need to use the latest biojava-live tree to have this example
working.

- Do not use multiple threads to send loads of requests to NCBI. This
would only get you into trouble, up to getting you blacklisted by NCBI.

The following sample program is slightly modified demo program from
biojava3-ws module's demo package:

```java import static
org.biojava.nbio.ws.alignment.qblast.BlastAlignmentParameterEnum.ENTREZ\_QUERY;
import java.io.\*; import
org.biojava.nbio.core.sequence.io.util.IOUtils; import
org.biojava.nbio.ws.alignment.qblast.\*;

public class NCBIQBlastServiceDemo {

`   private static final String BLAST_OUTPUT_FILE = "blastOutput.xml";    // file to save blast results to`  
`   private static final String SEQUENCE = "MKWVTFISLLFLFSSAYSRGVFRRDAHKSEVAHRFKDLGEENFKALVLIAFAQYLQQCP";     // Blast query sequence`

`   public static void main(String[] args) {`  
`       NCBIQBlastService service = new NCBIQBlastService();`

`       // set alignment options`  
`       NCBIQBlastAlignmentProperties props = new NCBIQBlastAlignmentProperties();`  
`       props.setBlastProgram(BlastProgramEnum.blastp);`  
`       props.setBlastDatabase("swissprot");`  
`       props.setAlignmentOption(ENTREZ_QUERY, "\"serum albumin\"[Protein name] AND mammals[Organism]");`

`       // set output options`  
`       NCBIQBlastOutputProperties outputProps = new NCBIQBlastOutputProperties();`  
`       // in this example we use default values set by constructor (XML format, pairwise alignment, 100 descriptions and alignments) `

`       // Example of two possible ways of setting output options`

// outputProps.setAlignmentNumber(200); //
outputProps.setOutputOption(BlastOutputParameterEnum.ALIGNMENTS, "200");

`       String rid = null;          // blast request ID`  
`       FileWriter writer = null;`  
`       BufferedReader reader = null;`  
`       try {`  
`           // send blast request and save request id`  
`           rid = service.sendAlignmentRequest(SEQUENCE, props);`

`           // wait until results become available. Alternatively, one can do other computations/send other alignment requests`  
`           while (!service.isReady(rid)) {`  
`               System.out.println("Waiting for results. Sleeping for 5 seconds");`  
`               Thread.sleep(5000);`  
`           }`

`           // read results when they are ready`  
`           InputStream in = service.getAlignmentResults(rid, outputProps);`  
`           reader = new BufferedReader(new InputStreamReader(in));`

`           // write blast output to specified file`  
`           File f = new File(BLAST_OUTPUT_FILE);`  
`           System.out.println("Saving query results in file " + f.getAbsolutePath());`  
`           writer = new FileWriter(f);`

`           String line;`  
`           while ((line = reader.readLine()) != null) {`  
`               writer.write(line + System.getProperty("line.separator"));`  
`           }`  
`       } catch (Exception e) {`  
`           System.out.println(e.getMessage());`  
`           e.printStackTrace();`  
`       } finally {`  
`           // clean up`  
`           IOUtils.close(writer);`  
`           IOUtils.close(reader);`

`           // delete given alignment results from blast server (optional operation)`  
`           service.sendDeleteRequest(rid);`  
`       }`  
`   }`

} ```
