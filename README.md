# *A*ntigen *R*eceptors *Res*earch *T*ool / ARResT


ARResT is designed to enable a deep understanding of antigen receptor sequences with a cascade of algorithms and databases. ARResT, in some form or other over the years, is behind all of our publications in the field, and will continue to be in the foreseeable future. It is under constant development by and hosted at the [Bioinformatics Analysis Team / BAT (i.e. us)](http://bat.infspire.org) and many colleagues and collaborators, including the [EuroClonality-NGS (EC-NGS) consortium](http://www.euroclonalityngs.org) on Next-Generation Sequencing for IG / TR immunoprofiling.<br>


Please visit http://bat.infspire.org/arrest/ for more,<br>and see below for what is currently available through this GitHub repository.


---


# ARResT/Interrogate
an interactive immunoprofiler for IG/TR NGS data




## In a few words
ARResT/Interrogate is a bioinformatics platform for immunoprofiling, i.e. the analysis of RepSeq data. It can process and annotate raw sequencing data for all relevant types of IG/TR rearrangements, store and retrieve results / reports / logs, parse IMGT/HighV-QUEST summary files, enable multiple select / filter / statistical queries on data and user-provided metadata, visualise, provide access to full sequences, enable detailed sequence analysis in the form of networks and alignments, export - under one interactive web browser-based interface.




## Citations and Demo server
cite us: http://www.ncbi.nlm.nih.gov/pubmed/27742700</br>
> **ARResT/Interrogate: an interactive immunoprofiler for IG/TR NGS data**<br>
> ###### Vojtech Bystry [1#], Tomas Reigl [1#], Adam Krejci [1,2#], Martin Demko [1], Barbora Hanakova [1], Andrea Grioni [1,3], Henrik Knecht [4], Max Schlitt [4], Peter Dreger [5], Leopold Sellner [5], Dietrich Herrmann [4], Marine Pingeon [6], Myriam Boudjoghra [6], Jos Rijntjes [7], Christiane Pott [4], Anton W. Langerak [8], Patricia J. T.A. Groenen [7], Frederic Davi [6], Monika Brüggemann [4] and Nikos Darzentas [1], also on behalf of EuroClonality-NGS<br>
> ###### _[1] CEITEC - Central European Institute of Technology, Masaryk University, Brno, Czech Republic, [2] RECAMO, Masaryk Memorial Cancer Institute, Brno, Czech Republic, [3] Centro Ricerca Tettamanti, Clinica Pediatrica, Università di Milano-Bicocca, Ospedale San Gerardo/Fondazione MBBM, Monza, Italy, [4] Department of Hematology, University Hospital Schleswig-Holstein, Campus Kiel, Kiel, Germany, [5] Department of Medicine V, University Hospital Heidelberg, Heidelberg, Germany, [6] Department of Hematology, Hopital Pitié-Salpêtrière and Pierre et Marie Curie University, Paris, France, [7] Department of Pathology, Radboud University Nijmegen Medical Center, Nijmegen, The Netherlands, [8] Department of Immunology, Erasmus MC, University Medical Center, Rotterdam, The Netherlands_


demo server: http://bat.infspire.org/arrest/interrogate/demo/</br>
> _The demo server currently only provides access to pre-processed data (click on blue button when you visit), i.e. we limit access to the ‘processing’ panel and to the functionalities of the ‘file’ panel (see below for more on panels). Please contact us at bat@infspire.org if we can help, e.g. by providing an account on our servers._




## Context
Immunoglobulins (IG) and T cell receptors (TR) are highly adaptive molecular receptors responsible for antigen recognition in immunological responses. Fundamental to their adaptiveness is their enormous inherent variability, achieved through stochastic processes during B and T cell maturation. The study of immunoglobulins and T cell receptors using next-generation sequencing has finally allowed exploring immune repertoires and responses in their immense variability and complexity. Producing and mining these inherently complex immunogenetic annotations, of usually millions of reads and tens to hundreds of samples, is a non-trivial task.


In ARResT/Interrogate, we put together in one platform features and functionalities we believe are needed for wide-ranging _in silico_ immunoprofiling. These insights are a result of collaborative efforts within the [EuroClonality-NGS (EC-NGS) consortium](http://www.euroclonalityngs.org) coordinated by Anton Langerak of Erasmus MC in Rotterdam, which strives to develop, standardize, and validate _in vitro_ assays and bioinformatics for IG/TR NGS analysis towards a wide variety of applications, many with their own needs:
- basic research,
- technology development e.g. primers and assays,
- diagnostic / clinical,
- MRD and clonality assessment and monitoring,
- repertoire studies.




## Overview
ARResT/Interrogate is primarily based on R and Perl, relies on external tools and packages, and uses Shiny for user interactivity and web-based accessibility. Its user interface is organised in four (4) main panels representing current logically-ordered major functionalities:


### ‘processing’
Interface to the processing, annotation and profiling pipeline, which turns FASTQ raw data into tabulated information.<br><br>
![alt text](http://bat.infspire.org/images/intrg-processing.png "‘processing’ panel")


### ‘file’
Loading of new, existing, stored results, including IMGT ‘summary’ files and user-defined highly-flexible tables (see our [Bioinformatics publication](http://www.ncbi.nlm.nih.gov/pubmed/27742700)); access to pipeline reports and logs; viewing and editing of sample metadata.<br><br>
![alt text](http://bat.infspire.org/images/intrg-file.png "‘file’ panel")


### ‘questions’
Data selection and filtering, comparative calculations, and visualization.<br><br>
![alt text](http://bat.infspire.org/images/intrg-questions.png "‘questions’ panel")


### ‘forensics’
Access to full nucleotide sequences; detailed sequence analysis with sequence networks and alignments; direct access to IMGT/V-QUEST.<br><br>
![alt text](http://bat.infspire.org/images/intrg-forensics.png "‘forensics’ panel")


There is a **‘help’** panel with a running example, but our current strategy is to provide help, hints and tips through text across the interface, mainly through hover-over tooltips (almost always marked with an ‘[?]’).


We have tagged **‘processing’** and **‘forensics’** as beta since they’re more actively in development, while **‘file’** and **‘questions’** have also been covered in our [Bioinformatics publication](http://www.ncbi.nlm.nih.gov/pubmed/27742700).




## A few more details on ‘processing’
The pipeline options available are organized in user-editable ‘scenarios’. Samples and their FASTQ files (including paired-ended and from multiple lanes, can be gzipped) can be uploaded, organized, annotated, and selected to be processed. The pipeline produces comprehensive reports, including detailed log files and messages that identify and even advise on potential issues.
#### primers
The pipeline is able to annotate reads with primer sequences provided by the user and keep this annotation for downstream analysis, e.g. run quality control. Primers can also be used to safeguard the completeness of the amplicon, by requiring that both 5’ and 3’ primers are located on each read.
#### species, germlines, junction classes, and clonotypes
Germlines sequences for all human IG/TR genes and alleles are sourced from IMGT (mainly from the IMGT/V-QUEST reference directory but also from IMGT/LIGM-DB for the complete D genes and alleles) by the ‘germinate.pl’ script - other species could be easily added, just let us know. The intron and Kde segments of the IGK locus are provided by partners from the EuroClonality-NGS consortium. The pipeline uses BWA-MEM to align germlines to reads and is able to identify rearrangements and junctions of all currently applicable types, which we call ‘junction classes’:
<pre>
<b>normal</b>
IG   VJ : Vh-(Dh)-Jh
IG   VJ : Vk-Jk
IG   VJ : Vl-Jl
TR   VJ : Va-Ja
TR   VJ : Va-Jd
TR   VJ : Vb-(Db)-Jb
TR   VJ : Vd-(Dd)-Ja
TR   VJ : Vd-(Dd)-Jd
TR   VJ : Vg-Jg
<b>incomplete</b>, not currently supported by IMGT
IG   DJ : Dh-Jh
TR   DD : Dd2-Dd3
TR   DJ : Db-Jb
TR   DJ : Dd2-Jd
TR   DJ : Dd-Ja
TR   VD : Vd-Dd3
<b>special</b>, not currently supported by IMGT
IG   INTRON-KDE
IG   Vk-KDE
</pre>
ARResT/Interrogate produces junction sequences even for incomplete and special rearrangements (as outlined above) by using specific triplets chosen in an educated way, without making any claim as to their biological or functional relevance. These junctional sequences do allow for consistent and detailed analysis across all junction classes.
<pre>
<b>anchors</b>
5'
| V segment      : C = TG[CT]
| D segment      : V = GT.       the last triplet of the 5' heptamer
| intron segment : P = CCC       a triplet before the heptamer
3'
| J segment      : W = TGG or F = TT[CT]
| D segment      : H = CA[CT]    the first triplet of the 3' heptamer
| Kde segment    : R = CGA       a triplet after the heptamer
</pre>
Finally, the pipeline assigns sequences to clonotypes, whose definition is user-settable - there is a lot of work and discussion about clonotype definitions, and EC-NGS will eventually provide guidelines which we will implement in ARResT/Interrogate. We currently provide four (4) options, all using junction classes and 5’ and 3’ gene assignments, then combined with nt or aa junction sequences, either per-sequence individual ones or based on supervised clustering - the current default is with cluster-based aa junctions. 
#### validation
The pipeline is validated against a set of (currently) 275 diverse sequences, from TP53 to non-rearranged germlines to examples of all aforementioned junction classes. Results are also compared against IMGT/V-QUEST when applicable, i.e. when junction classes are also supported by IMGT. The few current discrepancies are mostly restricted to differing 5’ and 3’ gene assignments, especially in cases with incompletely sequenced 5’ gene segments.
#### command-line
We encourage the use of the ‘processing’ panel to access the pipeline, but of course command-line access is available. The main (Perl) script is the ```pipeline/scripts/``` folder and called ```wmd.pl```. Just calling it provides help and a quick guide, but a minimal command would be ```wmd.pl --op``` in the folder with (gzipped) FASTQ/FASTA files, with results made available in the `...--results` folder - look for .clntab files and run ```wmd.pl --help clntab``` to get column names and descriptions.




## Installation


#### minimum HW requirements
CPU: >= 2, RAM: 2 GB, HDD: at least 200 MB


#### OS
**Ubuntu** or **Debian** for *local* or *server* version with **‘processing’**</br>
**macOS** or **Windows** for *local* version without **‘processing’**


#### R and required R libraries
at least 3.3.1
```
ConsensusClusterPlus (Bioconductor), Biostrings (Bioconductor), devtools, RCurl, grDevices, base64enc, plyr,
data.table, RColorBrewer, pROC, ROCR, ggthemes, fields, amap, dynamicTreeCut, showtext, stringi, gplots,
indicspecies, vegan, ggplot2, gdata, R.utils, curl, scales, nnet, MASS, reshape2, gtools, igraph, httpuv,
htmltools, magrittr, ff, ffbase, V8, htmlwidgets, shiny, DT, shinyjs, rCharts, shinyTree, visNetwork,
Rcpp
```


#### required Perl modules
```
CGI, CGI::Ajax, Data::Dumper, Digest::MD5, FindBin, Getopt::Long, Hash::Merge, IPC::Open2, LWP, LWP::Simple,
List::MoreUtils, List::Util, Math::Trig, Sort::Naturally, Spreadsheet::ParseExcel, Statistics::Descriptive,
Storable, threads, threads::shared
```


#### download and install ARResT/Interrogate locally on user's machine
Clone or download this repository and run ```sudo ./setup.pl --all --style [server|local|both]```. Use ```server``` for server-like machines with no GUI; ```local```, if you don't want to install shiny-server on your machine. Then...</br>
for *server*: the shiny-server app can be accessed in a web browser with the public IP address of the machine.
</br>or</br>
for *local*: double click **‘Run Interrogate’** on user's desktop, or run ```shiny::runApp("INTERROGATE_DOWNLOAD_FOLDER")``` in R.


#### launch Interrogate app directly from GitHub repository
#####(‘processing’ is disabled, and you need all required R libraries)
```
shiny::runGitHub("infspiredBAT/ARResT.Interrogate")
```




## External tools
We thank all the brilliant people who have created and made available these tools, without which ARResT/Interrogate wouldn’t have been possible.
<pre>
BWA | https://github.com/lh3/bwa | GPL-3.0
BioBloom:categorizer | https://github.com/bcgsc/biobloom | free for academic use (BCCA licence)
BioBloom:maker | https://github.com/bcgsc/biobloom | free for academic use (BCCA licence)
CAP3 | http://seq.cs.iastate.edu/cap3.html
FASTA v36 | http://faculty.virginia.edu/wrpearson/fasta/fasta36/ | Apache2.0 Open Source License
FLASh | https://ccb.jhu.edu/software/FLASH/ | OSI Certified Open Source Software
VSEARCH | https://github.com/torognes/vsearch | GPL-3.0
samtools | https://github.com/samtools/samtools | MIT
seq-align:Needleman-Wunsch | https://github.com/noporpoise/seq-align | Public Domain
swarm | https://github.com/torognes/swarm | AGPL-3.0
</pre>




## Acknowledgements & Funding
We gratefully acknowledge all our partners and collaborators, who have helped the inception, development, and publication of ARResT/Interrogate.
Funding by Ministry of Health of the Czech Republic grant nr. 16-34272A, project CEITEC 2020 (LQ1601), project MEYS-NPS I-LO1413, and ESLHO::EuroClonality. Computational resources by MetaCentrum (LM2010005) and CERIT-SC (CZ.1.05/3.2.00/08.0144).


