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
for file in dre*; do sed 's/^ *//' "$file" >> dre.txt; echo $file; done
```
