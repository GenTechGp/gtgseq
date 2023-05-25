# Open Data from Genomic Technologies Group

You can browser browse the gtgseq AWS S3 bucket by following [https://gtgseq.s3.amazonaws.com/index.html](https://gtgseq.s3.amazonaws.com/index.html) on your broswer. Alternatively, you can use the aws cli:
```
aws s3 ls --no-sign-request s3://gtgseq/
```

Structure:
```
- ont-r10-dna
  |_ NA24385
  |  |_ raw
  |  |  |_PGXX22394_reads.blow5
  |  |  |_PGXX22394_reads.blow5.idx
  |  |_ analyses
  |     |_basecalls
  |       |_guppy642hac
  |         |_PGXX22394_guppy642hac.fastq.gz
  |         |_PGXX22394_guppy642hac_mm217.bam
  |         |_PGXX22394_guppy642hac_mm217.bam.bai 
  |     |_methcalls
  |       |_f5c12
  |       |  |_PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz
  |       |_...dorado_remora?
  |_......... 
  
- pb-revio
  ....
```

Downloading a file can be done using the web browser; a CLI tool such as wget, curl or axel; or, aws cli. Downloading through aws cli is faster and recommended, especially for larger files.

Example using wget:
```
wget https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5
```

Example using aws cli:
```
aws s3 cp --no-sign-request s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 ./
```

If you are doing your compute on AWS or if you have a very-high bandwidth and very-low latency Internet connection, you may mount the S3 bucket and then directly access as explained [here](docs/mount.md).

Datasets are explained [here](docs/data.md).

# Acknowledgement

AWS Open Data Sponsorship Program for generously hosting this open data.
