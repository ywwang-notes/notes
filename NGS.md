### Fastq
* a fast way to count reads: `echo $(cat filename.fastq|wc -l)/4|bc`
* useful commands: `head`, `tail`, `ls -hl`
* search a pattern: `grep "some pattern" filename.fastq` (better use after converting fastq into tabbed table)
* fastq to tabbed table: `cat filename.fastq | paste - - - - > filename.txt`
* pattern matching: `awk '/some pattern/ {Actions}' filename`
  * `awk '/CCCC/' {print $1 "\t" $3}' filename.txt`
* misc
  * `sed 's/^ *//' output.txt | more`
  * `awk '/\../ {print $1 "\t" $2}' output.txt | sed 's/\.//g' | tr [:lower:] [:upper:] | more`
  * `for file in *.pdf; do pdftotext -layout "$file" "$(basename $file .pdf).txt"; done`
* example
```
for file in *.pdf; do pdftotext -layout "$file" "txt/$(basename $file .pdf).txt"; echo $file; done
for file in dre*.txt; do sed 's/^ *//' $file | awk '/\.\./ {print $1 "\t" $2}' | sed 's/\.//g' | sed '/^(/d' | tr [:lower:] [:upper:] >> dre.txt; echo $file; done
# 1. ignore blank; b. select ... lines; c. remove "..."; d. capitalize sequences
```
