# wiki
Only the wiki section of the project will be populated with the solutions to my day to day life hurdle with bioinfo - be it the installation of a software, or a very general aspect that I faced during preparing or running a script. I am just a human and won't be able to remember all the solutions that I already found, therefore, I am going to compile them here.


1. GATK related resources on hg19 (be it the genome assembly or the CNV blacklist or even the panel-of-normal for mutect2) is available here: https://console.cloud.google.com/storage/browser/gatk-best-practices/somatic-b37
click on the file, load the page and download first then transfer to the server of yours.

2. Someties (I found most of the time), phython2 is the default version in your machinee. But some programs are built on python3. Therefore, you need to run them specifing "python3" to begin with as only "python" refers to  "/user/bin/python" or "/user/bin/python2". One solution is to alias the python3 to python (alias python=python3) and put in the ~/.bashhrc or ~/.bash_aliases files. Then run "source  ~/.bashhrc" or "source ~/.bash_aliases"
or simply run the command on the terminal -
"alias python=python3"

3. A big headache appeared as some of the previously reported mutations on AR (non-synonymous) were missing from the final annotation of Clonal events. It appeared that they were not accounted for by Sclust as these mutations are not labelled as PASS, rather than labelled as clustered_event. For example on ChrX, a mutation at 66943552 is phased with another mutation at 66943543 and Mutect2 was considering as clustered event. Inerestingly, there were reports of them on the same read in some reads and otherwise for some other. According to the MuTect2 definition, this kind of mutation calls are potential artefacts, but reported to be real by other groups. Then, I found a suggestion to use GATK4 Mutect2 on https://github.com/broadinstitute/gatk-protected/issues/773. A test run on tumour against Broad Institute's PON with this GATK4 Mutect2 on ChrX proved to be usefull and the mutation at ChrX:66943552 is reported PASS.
N.B. It was still reported as clustered_event by GATK3 MuTect2 against PON (with or without a matched normal).

4. Here's a mini description about a very useful software repository / utility toolkit called **"BamUtil"** to modify or parse crucial data from a SAM or BAM file -

The software reads the beginning of an input file to determine if it is SAM/BAM. To determine the format (SAM/BAM) of the output file, the software checks the output file's extension. If the extension is ".bam" it writes a BAM file, otherwise it writes a SAM file.

BamUtil is built using libStatGen. Running bin/bam with no parameters will print the usage information for the bam executable. Running bin/bam subProgram will print the usage information for the BamUtil sub-program.

**Tools to Rewrite SAM/BAM Files:**
convert - Convert SAM/BAM to SAM/BAM (optionally converts between '=' & bases in the sequence
writeRegion - Write a file with reads in the specified region and/or have the specified read name
splitChromosome - Split BAM into 1 file per Chromosome
splitBam - Split BAM into 1 file per Read Group
findCigars - Output just the reads that contain any of the specified CIGAR operations.
BAM Recovery - Recover corrupted BAM files
**Tools to Modify & write SAM/BAM Files:**
clipOverlap - Clip overlapping read pairs in a SAM/BAM File already sorted by Coordinate or ReadName so they do not overlap
filter - Filter reads by soft clipping ends with too high of a mismatch percentage and by marking reads unmapped if the quality of mismatches is too high
revert - Revert SAM/BAM replacing the specified fields with their previous values (if known) and removes specified tags
squeeze - Reduce file size by dropping OQ fields, duplicates, & specified tags, using '=' when a base matches the reference, binning quality scores, and replacing readNames with unique integers
trimBam - Trim the ends of reads in a SAM/BAM file changing read ends to 'N' and quality to '!' or by doing soft clips
mergeBam - Merge multiple BAMs and headers appending ReadGroupIDs if necessary
polishBam - Add/update header lines & add the RG tag to each record
dedup - Mark or remove duplicates, can also perform recalibration
recab - Recalibrate base qualities
**Informational Tools:**
validate - Validate a SAM/BAM File, checking file format & printing statistics
diff - Diff 2 coordinate sorted SAM/BAM files.
stats - Generate some basic statistics for a SAM/BAM file
gapInfo - Print information on the gap between read pairs in a SAM/BAM File.
**Helper Tools to Print Information In Readable Format:**
dumpHeader - Print the SAM/BAM Header to the screen
dumpRefInfo - Print SAM/BAM Reference Name Information from the header
dumpIndex - Print BAM Index File to the screen in a readable format
readReference - Print the reference string for the specified region to the screen
explainFlags - Describe SAM/BAM flags
**Additional Tools:**
bam2FastQ - Convert the specified BAM file to fastQs.
**Dummy/Example Tools:**
readIndexedBam - Read an indexed BAM file reference by reference id -1 to the max reference id and write it out as a SAM/BAM file
