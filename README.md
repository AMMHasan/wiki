# wiki
Only the wiki section of the project will be populated with the solutions to my day to day life hurdle with bioinfo - be it the installation of a software, or a very general aspect that I faced during preparing or running a script. I am just a human and won't be able to remember all the solutions that I already found, therefore, I am going to compile them here.


1. GATK related resources on hg19 (be it the genome assembly or the CNV blacklist or even the panel-of-normal for mutect2) is available here: https://console.cloud.google.com/storage/browser/gatk-best-practices/somatic-b37
click on the file, load the page and download first then transfer to the server of yours.

2. Someties (I found most of the time), phython2 is the default version in your machinee. But some programs are built on python3. Therefore, you need to run them specifing "python3" to begin with as only "python" refers to  "/user/bin/python" or "/user/bin/python2". One solution is to alias the python3 to python (alias python=python3) and put in the ~/.bashhrc or ~/.bash_aliases files. Then run "source  ~/.bashhrc" or "source ~/.bash_aliases"

or simply run the command on the terminal -
alias python=python3


