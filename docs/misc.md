# Miscellaneous

This document briefly describes what is in the [https://gtgseq.s3.amazonaws.com/index.html#misc](https://gtgseq.s3.amazonaws.com/index.html#misc/) directory. 
Note that you should be familiar with the information documented in the [README](../README.md) and the [datasets](datasets.md) before going through this document.

Misc has two subdirectories:
1. sub: contains smaller subsets of the bigger datasets 
2. rid: lists of read IDs for selected chromosomes (useful for grabbing through slow5curl)

Note that only selected datasets would have these miscellaneous data and are added upon request. The file names would have the identifier which can be related to its parent BLOW5 file. For instance any miscellaneous data files for the parent BLOW5 file named PGXXSX240041reads.blow5 would contain PGXXSX240041 in the file name. 
500k in a file name refers to 500,000 randomly sampled reads, 20k refers to 20,000 randomly sampled reads.  chr22 for instance means that the reads mapping to chr22.
