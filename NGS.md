### Questions
* transcribed fragments (precursor, pri-RNA, protein-bound RNA, etc)? All 

### Basics
  * [NYU Next-Generation Sequencing Analysis Resources](https://learn.gencore.bio.nyu.edu/)  
  * [Fastq](https://learn.gencore.bio.nyu.edu/ngs-file-formats/quality-scores/)
  * [Quality Score Encoding](https://support.illumina.com/help/BaseSpace_OLH_009008/Content/Source/Informatics/BS/QualityScoreEncoding_swBS.htm)
  * [Three-letter prefix](https://www.genome.jp/kegg/catalog/org_list.html)
### Welgene
* [TRIzol Reagent](https://www.thermofisher.com/order/catalog/product/15596026#/15596026)
* [QIAseq miRNA Library Kit](https://www.qiagen.com/tw/products/discovery-and-translational-research/next-generation-sequencing/metagenomics/qiaseq-mirna-ngs/?clear=true#productdetails): [AACTGTAGGCACCATCAAT](https://www.qiagen.com/us/resources/faq?id=f12b85b4-df4f-43b5-9e82-a4fd0ddbdcc0&lang=en); [Illumina adapter sequences](https://sapac.support.illumina.com/downloads/illumina-adapter-sequences-document-1000000002694.html)
* [RNA 6000 labchip kit](https://ipmb.sinica.edu.tw/microarray/workshop/workshop-11.pdf)

### CLC
* [Biomedical Genomics Analysis](https://resources.qiagenbioinformatics.com/manuals/biomedicalgenomicsanalysis/current/index.php?manual=Introduction.html) 
  * Ready to use workflows: QIAseq miRNA Quantification, QIAseq miRNA Differential Expression
  * Tools: QIASeq miRNA expert tools / Create UMI Reads for miRNA
* Tools: 
  [Map Reads to Reference](http://resources.qiagenbioinformatics.com/manuals/clcgenomicsworkbench/900/index.php?manual=Exploring_novel_miRNAs.html), 
  RNA-Seq and small RNA analysis / miRNA analysis / Quantify miRNA; RNA-Seq Analysis (for unmapped reads)

### miRNA-seq data processing
* [QIAseq® miRNA Primary Quantification](https://www.qiagen.com/us/resources/resourcedetail?id=bea2dcfa-0a5c-47c5-afd8-8b0fe90a471a&lang=en)
* Trimmomatic
```
$@.fastq $@-trim.fastq ILLUMINACLIP:/mnt/d/Project/Trimmomatic-0.39/adapters/QIAseq.fa:2:30:10 -trimlog $@-trim.log SLIDINGWINDOW:4:15
```
* miRNA prediction: chapter 6 in Computational Epigenetics and Diseases

### Un-sorted
DeSeq, miRNA 19-d, [DAVID functional annotation](https://david.ncifcrf.gov/summary.jsp)

### Ubuntu commands
* a fast way to count reads: `echo $(cat filename.fastq|wc -l)/4|bc`
* useful commands: `head`, `tail`, `ls -hl`
* search a pattern: `grep "some pattern" filename.fastq` (better use after converting fastq into tabbed table)
* fastq to tabbed table: `cat filename.fastq | paste - - - - > filename.txt`
* pattern matching: `awk '/some pattern/ {Actions}' filename`
  * `awk '/CCCC/ {print $1 "\t" $3}' filename.txt`
* misc
  * `sed 's/^ *//' output.txt | more`
  * `awk '/\../ {print $1 "\t" $2}' output.txt | sed 's/\.//g' | tr [:lower:] [:upper:] | more`
  * `for file in *.pdf; do pdftotext -layout "$file" "$(basename $file .pdf).txt"; done`
  * `sort -t, -k4,4 filename`: file contains comma separated columns; sort by 4th to 4th column(s)  
  * `awk -F',' '{print $4}' file | sort -u`: extract unique elements from the 4th column in a comma-separated file
  * `sed $'s/[^[:print:]\t]//g' < input > outout`: remove special characters
* examples
```
for file in *.pdf; do pdftotext -layout "$file" "txt/$(basename $file .pdf).txt"; echo $file; done
for file in dre-*.txt; do sed 's/^ *//' $file | awk -v src=$file '/\.\./ {print $1 "\t" $2 "\t" src}' | sed 's/\.//g' | sed '/^(/d' | tr [:lower:] [:upper:] >> dre.txt; echo $file; done
# 1. ignore blank; b. select ... lines; c. remove "..."; d. capitalize sequences
```
