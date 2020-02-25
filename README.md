# wiki
Only the wiki section of the project will be populated with the solutions to my day to day life hurdle with bioinfo - be it the installation of a software, or a very general aspect that I faced during preparing or running a script. I am just a human and won't be able to remember all the solutions that I already found, therefore, I am going to compile them here.


1. GATK related resources on hg19 (be it the genome assembly or the CNV blacklist or even the panel-of-normal for mutect2) is available here: https://console.cloud.google.com/storage/browser/gatk-best-practices/somatic-b37
click on the file, load the page and download first then transfer to the server of yours.

2. Someties (I found most of the time), phython2 is the default version in your machinee. But some programs are built on python3. Therefore, you need to run them specifing "python3" to begin with as only "python" refers to  "/user/bin/python" or "/user/bin/python2". One solution is to alias the python3 to python (alias python=python3) and put in the ~/.bashhrc or ~/.bash_aliases files. Then run "source  ~/.bashhrc" or "source ~/.bash_aliases"
or simply run the command on the terminal -
"alias python=python3"

3. A big headache appeared as some of the previously reported mutations on AR (non-synonymous) were missing from the final annotation of Clonal events. It appeared that they were not accounted for by Sclust as these mutations are not labelled as PASS, rather than labelled as clustered_event. For example on ChrX, a mutation at 66943552 is phased with another mutation at 66943543 and Mutect2 was considering as clustered event. Inerestingly, there were reports of them on the same read in some reads and otherwise for some other. According to the MuTect2 definition, this kind of mutation calls are potential artefacts, but reported to be real by other groups. Then, I found a suggestion to use GATK4 Mutect2 on https://github.com/broadinstitute/gatk-protected/issues/773. A test run on tumour against Broad Institute's PON with this GATK4 Mutect2 on ChrX proved to be usefull and the mutation at ChrX:66943552 is reported PASS.
N.B. It was still reported as clustered_event by GATK3 MuTect2 against PON (with or without a matched normal).
