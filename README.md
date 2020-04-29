# Fosmids
## Requirements
1. Python version 2
2. BLAST
## Code to merge the fosmids
```
# fosmids.fasta has all the fosmids sequence to be merged
module load blast/2.7.1+
blastn \
  -query fosmids.fasta \
  -subject fosmids.fasta \
  -outfmt "6 length pident nident mismatch gapopen gaps qseqid qstart qend qlen sseqid sstart send slen sstrand" > \
  blast.txt
 
# blast.txt is the output from the blast output
# blast_edited.txt is the blast
# fosmid_groups.txt are a txt file with fosmids that belong together
# fosmids_to_ignore.txt are a txt file with fosmids that should be ignored
# fosmids_to_merge.txt are a txt file with fosmids that are being merged
# fosmids.fasta is the input fasta
# merged_fosmids.fasta is the output fasta
# 5000 the minimum number of bases to overlap
# 1 is the maximum allowed errors
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
 
# fosmids_to_ref.sorted.bam is the bam file with the fosmids aligned
# fosmids_to_ref_grouped.sorted.bam is the bam file with the fosmids that are to be merged
# fosmid_groups.txt is the output from above
python python/add_read_group.py \
  fosmids_to_ref.sorted.bam \
  fosmids_to_ref_grouped.sorted.bam \
  fosmid_groups.txt
samtools index fosmids_to_ref_grouped.sorted.bam

```
