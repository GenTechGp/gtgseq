# Garvan Institute Long Read Sequencing Benchmark Data

This repository contains the documentation for the long read sequencing data from the Genomic Technologies Group at Garvan Institute of Medical Research.

Currently, the dataset contains two reference datasets that will be useful for benchmarking and comparing bioinformatics tools for genome analysis. The two datasets are NA12878 (HG001) and NA24385 (HG002), sequenced on an Oxford Nanpopore Technologies (ONT) PromethION using the latest R10.4.1 flowcells. Raw signal data output by the sequencer is provided for these datasets in [BLOW5 format](https://www.nature.com/articles/s41587-021-01147-4), and can be rebasecalled when basecalling software updates bring accuracy and feature improvements over the years. Raw signal data is not only for rebasecalling, but also can be used for emerging bioinformatics tools that directly analyse raw signal data. We also provide the basecalled data alongside the raw signal data and will continue to provide updated basecalls when there is a major update to the basecalling software. 

In the future, we plan to extend this open dataset with additional samples, including sequencing runs from vendors other than ONT. 
 
## Dataset location

You can browser browse the gtgseq AWS S3 bucket by following [https://gtgseq.s3.amazonaws.com/index.html](https://gtgseq.s3.amazonaws.com/index.html) on your broswer. Alternatively, you can use the aws cli:
```
aws s3 ls --no-sign-request s3://gtgseq/
```

## Structure

An example of the directory structure in the AWS S3 bucket is given below, for the sample NA24385. The `raw` directory will contain the BLOW5 file and BLOW5 file index for random acesss. The `analyses` directory will contain data such as basecalls and modcalls. In this example, `basecalls` contain the default qscore passed high accuracy (hac) basecalls from Guppy 6.4.2 in bgzip compressed FASTQ format. Those reads aligned to the hg38_noAlt.fa reference using minimap2 2.14 is also available in BAM format. BAM index is also provided for region access. The `modcalls` contains the CpG methylation frequencies from f5c 1.2.

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
  |     |_modcalls
  |       |_f5c12
  |       |  |_PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz
  |       |_...
  |_......... 
  
```

Datasets and files are explained [here](docs/data.md) along with metadata.

#  Downloading

Downloading a file can be done using the web browser; a CLI tool such as wget, curl or axel; or, aws cli. Downloading through aws cli is faster and recommended, especially for larger files.

Example using wget:
```
wget https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5
```

Example using aws cli:
```
aws s3 cp --no-sign-request s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 ./
```

#  Mounted Access

If you are doing your compute on AWS or if you have a very-high bandwidth and very-low latency Internet connection, you may mount the S3 bucket and then directly access as explained [here](docs/mount.md).

# Other public datasets

If you are interested in the previous nanopore chemistry R9.4.1, links to such data is available [here](https://github.com/hasindu2008/seq/#ont-r941-chemistry). 

# Acknowledgement

AWS Open Data Sponsorship Program for generously hosting this open data.
