# Fosmids
## Requirements
1. Python version 2
## Code to merge the fosmids
```
module load blast/2.7.1+
blastn \
  -query fosmids.fasta \
  -subject fosmids.fasta \
  -outfmt "6 length pident nident mismatch gapopen gaps qseqid qstart qend qlen sseqid sstart send slen sstrand" > \
  blast.txt
  
python python/merge_fosmids.py 
  blast.txt \
  blast_edited.txt \
  fosmid_groups.txt \
  fosmids_to_ignore.txt \
  fosmids_to_merge.txt \
  fosmids.fasta \
  merged_fosmids.fasta \
  5000 \
  1

```
