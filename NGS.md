### Questions
* transcribed fragments (precursor, pri-RNA, protein-bound RNA, etc)? All 

### Protocol
* adapter?
* library prep: length selection?
* reads: 75SE?
* Quality report

### Gino
* [TRIzol Reagent](https://www.thermofisher.com/order/catalog/product/15596026#/15596026)
* [QIAseq miRNA Library Kit](https://www.qiagen.com/tw/products/discovery-and-translational-research/next-generation-sequencing/metagenomics/qiaseq-mirna-ngs/?clear=true#productdetails): [AACTGTAGGCACCATCAAT](https://www.qiagen.com/us/resources/faq?id=f12b85b4-df4f-43b5-9e82-a4fd0ddbdcc0&lang=en)
* [RNA 6000 labchip kit](https://ipmb.sinica.edu.tw/microarray/workshop/workshop-11.pdf)

### Basics
[NYU Next-Generation Sequencing Analysis Resources](https://learn.gencore.bio.nyu.edu)

### Fastq
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
* example
```
for file in *.pdf; do pdftotext -layout "$file" "txt/$(basename $file .pdf).txt"; echo $file; done
for file in dre-*.txt; do sed 's/^ *//' $file | awk -v src=$file '/\.\./ {print $1 "\t" $2 "\t" src}' | sed 's/\.//g' | sed '/^(/d' | tr [:lower:] [:upper:] >> dre.txt; echo $file; done
# 1. ignore blank; b. select ... lines; c. remove "..."; d. capitalize sequences
```
