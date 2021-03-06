---
title: BioJava:CookBook:Interfaces:ViewInGUI2
permalink: wiki/BioJava%3ACookBook%3AInterfaces%3AViewInGUI2
---

When building a bioinformatics GUI you will probably want to display the
sequence of residues and features in the Sequence you are displaying.
BioJava contains a number of GUI components that can render various
aspects of a Sequence.

The basic unit of any Sequence based GUI is the SequenceRenderContext
which holds the Sequence and sends instructions to a SequenceRenderer
which does the actual drawing of the Sequence. There are several
SequenceRenderer implementations in BioJava.

The following program demonstrates how to load an EMBL sequence file as
a RichSequence. Two SequenceRenderers are generated from this
RichSequence both filtered for CDS features and then filtered again for
either forward or reverse strand orientation. These are added to a
MultiLineRenderer as are a RulerRenderer and a SymbolSequenceRenderer.
The RulerRenderer displays the sequence coordinates and the
SymbolSequenceRenderer displays the sequence. The sequence display is
limited by the sequenceScale parameter of the TranslatedSequencePanel
and so is not always visible.

Once loaded, the sequence and CDS features displayed can be controlled
by the buttons in the JPanel controlPanel. These use the
setSequenceScale and setSymbolTranslation methods of the
TranslatedSequencePanel to modify the view.

Lastly, there is a SequenceViewerMotionListener added to the
TranslatedSequencePanel which triggers a ToolTip to display the name of
the gene when the mouse is over a CDS feature.

![](Viewer ScreenShot.JPG "fig:Viewer ScreenShot.JPG") ```java /\*\*

`* Class to load an EMBL sequence file and display it in a viewer.`  
`*/`

//Java libraries import java.awt.\*; import java.awt.event.\*; import
java.io.\*; import java.util.\*; import javax.swing.\*; //BioJava
libraries import org.biojava.bio.\*; import org.biojava.bio.seq.\*;
import org.biojava.bio.gui.sequence.\*; //BioJava extension libraries
import org.biojavax.\*; import org.biojavax.ontology.\*; import
org.biojavax.bio.seq.\*;

public class DisplaySequenceFile extends JFrame implements
SequenceViewerMotionListener {

` private TranslatedSequencePanel tsp = new TranslatedSequencePanel();`  
` private MultiLineRenderer mlr = new MultiLineRenderer();`  
` private RulerRenderer rr = new RulerRenderer();`  
` private SequenceRenderer seqr = new SymbolSequenceRenderer();`  
` private FeatureBlockSequenceRenderer fbsr;`  
` private RichSequence richSeq;`

` private Container con;`  
` private JPanel controlPanel;`  
` private JButton mvLeft, mvRight, zoomIn, zoomOut;`  
` private double sequenceScale = 0.05;`  
` private int windowWidth = 1200;`  
` private int windowHeight = 200;`

` public DisplaySequenceFile(String fileName){`  
`   super("Display Rich Sequence File");`  
`   //Load the sequence file`  
`   try {`  
`     richSeq = RichSequence.IOTools.readEMBLDNA(new BufferedReader(new FileReader(new File(fileName))), null).nextRichSequence();`  
`   }`  
`   catch (BioException bioe){`  
`     System.err.println("Not an EMBL sequence");`  
`   }`  
`   catch(FileNotFoundException fnfe){`  
`      System.err.println("FileNotFoundException: " + fnfe);`  
`   }`  
`   catch (IOException ioe){`  
`     System.err.println("IOException: " + ioe);`  
`   }`

`   //Define the appearance of the rendered Features`  
`   BasicFeatureRenderer bfr = new BasicFeatureRenderer();`  
`   GradientPaint gradient = new GradientPaint(0, 10, Color.RED, 0, 0, Color.white, true);`  
`   bfr.setFill(gradient);`  
`   bfr.setOutline(Color.RED);`

`   //Form a bridge between Sequence rendering and Feature rendering`  
`   fbsr = new FeatureBlockSequenceRenderer(bfr);`  
`   fbsr.setCollapsing(false);`

`   //Filter for CDS features on the forward strand`  
`   SequenceRenderer fwd_sr = new FilteringRenderer(fbsr,`  
`           new FeatureFilter.And(new FeatureFilter.ByType("CDS"),`  
`           new FeatureFilter.StrandFilter(StrandedFeature.POSITIVE)),`  
`           true);`  
`   //Filter for CDS features on the reverse strand`  
`   SequenceRenderer rev_sr = new FilteringRenderer(fbsr,`  
`           new FeatureFilter.And(new FeatureFilter.ByType("CDS"),`  
`           new FeatureFilter.StrandFilter(StrandedFeature.NEGATIVE)),`  
`           true);`

`   //Add the renderers to the MultiLineRenderer`  
`   mlr.addRenderer(fwd_sr);`  
`   mlr.addRenderer(rr);`  
`   mlr.addRenderer(rev_sr);`  
`   mlr.addRenderer(seqr);`

`   //Set the sequence renderer for the TranslatedSequencePanel`  
`   tsp.setRenderer(mlr);`  
`   //Set the sequence to render`  
`   tsp.setSequence(richSeq);`  
`   //Set the position of the displayed sequence`  
`   tsp.setSymbolTranslation(1);`  
`   //Set the scale as pixels per Symbol.`  
`   tsp.setScale(sequenceScale);`

`   //Add a sequence viewer motion listener to the TranslatedSequencePanel`  
`   tsp.addSequenceViewerMotionListener(this);`

`   //Generate the control panel`  
`   controlPanel = new JPanel();`  
`   controlPanel.setBackground(Color.lightGray);`  
`   //Move along the sequence towards 5' end`  
`   mvLeft = new JButton("<<");`  
`   mvLeft.addActionListener(new ActionListener(){`  
`     public void actionPerformed(ActionEvent ae){`  
`       int rightSide = tsp.getRange().getMax();`  
`       int leftSide = tsp.getRange().getMin();`  
`       int newStartPoint = leftSide - (rightSide - leftSide);`  
`       if (newStartPoint < 1){`  
`         newStartPoint = 1;`  
`       }`  
`       tsp.setSymbolTranslation(newStartPoint);`  
`     }`  
`   });`  
`   //Move along the sequence towards 3' end`  
`   mvRight = new JButton(">>");`  
`   mvRight.addActionListener(new ActionListener(){`  
`     public void actionPerformed(ActionEvent ae){`  
`       int rightSide = tsp.getRange().getMax();`  
`       int leftSide = tsp.getRange().getMin();`  
`       int screenWidth = rightSide - leftSide;`  
`       if ((rightSide + screenWidth) >= richSeq.length()){`  
`         tsp.setSymbolTranslation(richSeq.length() - screenWidth);`  
`       }`  
`       else {`  
`         tsp.setSymbolTranslation(rightSide);`  
`       }`  
`     }`  
`   });`  
`   //Increase sequence scale`  
`   zoomIn = new JButton("+");`  
`   zoomIn.addActionListener(new ActionListener(){`  
`     public void actionPerformed(ActionEvent ae){`  
`       sequenceScale = sequenceScale * 2;`  
`       //if sequence scale = 12 the bases are rendered`  
`       //no need to zoom in further so disable the button.`  
`       if (sequenceScale > 12){`  
`         sequenceScale = 12;`  
`         zoomIn.setEnabled(false);`  
`       }`  
`       tsp.setScale(sequenceScale);`  
`     }`  
`   });`  
`   //Reduce sequence scale`  
`   zoomOut = new JButton("-");`  
`   zoomOut.addActionListener(new ActionListener(){`  
`     public void actionPerformed(ActionEvent ae){`  
`       sequenceScale = sequenceScale / 2;`  
`       //if sequence scale is below 12 the enable zoomIn button`  
`       if (sequenceScale < 12){`  
`         zoomIn.setEnabled(true);`  
`       }`  
`       //If the scale allows more than the sequence to be displayed`  
`       //display the whole sequence`  
`       if (sequenceScale < ((double)tsp.getWidth()/(double)richSeq.length())){`  
`         sequenceScale = (double)tsp.getWidth()/(double)richSeq.length();`  
`         tsp.setSymbolTranslation(1);`  
`       }`  
`       tsp.setScale(sequenceScale);`  
`       //If the new scale coupled with the current SymbolTranslation means the`  
`       //displayed sequence can't fill the TranslatedSequencePanel then reset `  
`       //the SymbolTranlstion to allow for this`  
`       if(tsp.getRange().getMax() >= richSeq.length()){`  
`         int tmp = (int)((double)tsp.getWidth()/sequenceScale);`  
`         tsp.setSymbolTranslation(richSeq.length() - tmp);`  
`       }`  
`     }`  
`   });`  
`   controlPanel.add(mvLeft);`  
`   controlPanel.add(mvRight);`  
`   controlPanel.add(zoomIn);`  
`   controlPanel.add(zoomOut);`

`   con = new Container();`  
`   con = getContentPane();`  
`   con.setLayout(new BorderLayout());`  
`   con.add(controlPanel, BorderLayout.NORTH);`  
`   con.add(tsp, BorderLayout.CENTER);`  
`   setLocation(50,50);`  
`   setSize(windowWidth,windowHeight);`  
`   setVisible(true);`  
`   setResizable(false);`  
` }`

` /**`  
`  * Detect mouse dragged events`  
`  * @param sve`  
`  */`  
` public void mouseDragged(SequenceViewerEvent sve) {`  
` }`

` /**`  
`  * Detect mouse mouse moved events`  
`  * If the mouse moves over a CDS feature create a tooltiptext stating the`  
`  * the name of the gene associated with the CDS feature.`  
`  * @param sve`  
`  */`  
` public void mouseMoved(SequenceViewerEvent sve) {`  
`   //Manage the tooltip`  
`   ToolTipManager ttm = ToolTipManager.sharedInstance();`  
`   ttm.setDismissDelay(2000);`  
`   //If the mouse have moved over a SimpleFeatureHolder`  
`   if (sve.getTarget() instanceof SimpleFeatureHolder){`  
`     ComparableTerm gene = RichObjectFactory.getDefaultOntology().getOrCreateTerm("gene");`  
`     SimpleFeatureHolder sfh = (SimpleFeatureHolder)sve.getTarget();`  
`     FeatureHolder fh = sfh.filter(new FeatureFilter.ByType("CDS"));`  
`     Iterator `<RichFeature>` i =  fh.features();`  
`     while(i.hasNext()){`  
`       RichFeature rf = i.next();`  
`       RichAnnotation anno = (RichAnnotation) rf.getAnnotation();`  
`       Set annotationNotes = anno.getNoteSet();`  
`       for (Iterator `

<Note>
it = annotationNotes.iterator(); it.hasNext();) {

`         Note note = it.next();`  
`         if (note.getTerm().equals(gene)) {`  
`           tsp.setToolTipText("Gene: " + note.getValue());`  
`         }`  
`       }`  
`     }`  
`   }`  
`   else {`  
`     //Remove the tooltip`  
`     ttm.setDismissDelay(10);`  
`   }`  
` }`

` /**`  
`  * Main method`  
`  * @param args`  
`  */`  
` public static void main(String args []){`  
`   if (args.length == 1){`  
`     new DisplaySequenceFile(args[0]);`  
`   }`  
`   else {`  
`     System.out.println("Usage: java SequenceViewer `<EMBL file>`");`  
`     System.exit(1);`  
`   }`  
` }`

} ```
