# Garvan Institute Long Read Sequencing Benchmark Data

- This repository contains the documentation for the long read sequencing benchmark data from the [Genomic Technologies Group at Garvan Institute of Medical Research](https://www.garvan.org.au/research/labs-groups/genomic-technologies-lab). 
- S3 Bucket location: [https://gtgseq.s3.amazonaws.com/index.html](https://gtgseq.s3.amazonaws.com/index.html) <br>
- **The samples are detailed [here](docs/data.md), but make sure you first read the sections [Dataset location](#dataset-location), [Structure](#structure).**

## Introduction

The dataset contains reference samples that will be useful for benchmarking and comparing bioinformatics tools for genome analysis. Examples include: NA12878 (HG001) and NA24385 (HG002) sequenced on an Oxford Nanpopore Technologies (ONT) PromethION using the latest R10.4.1 flowcells; and, UHR RNA (direct-RNA) on an ONT PromethION using the latest RNA004 flowcells.  Raw signal data output by the sequencer is provided for these datasets in [BLOW5 format](https://www.nature.com/articles/s41587-021-01147-4), and can be rebasecalled when basecalling software updates bring accuracy and feature improvements over the years. 

## Citation

Please cite the following in your publications when using this dataset:

> Bonson Wong, James M Ferguson, Jessica Y Do, Hasindu Gamaarachchi, Ira W Deveson, Streamlining remote nanopore data access with slow5curl, GigaScience, Volume 13, 2024, giae016, https://doi.org/10.1093/gigascience/giae016

```
@article{10.1093/gigascience/giae016,
    title="{Streamlining remote nanopore data access with slow5curl}",
    author={Wong, Bonson and Ferguson, James M and Do, Jessica Y and Gamaarachchi, Hasindu and Deveson, Ira W},
    journal={GigaScience},
    volume={13},
    pages={7},
    year={2024},
    publisher={Oxford University Press},
}
```

Every BLOW5 file in this repository is also deposited to SRA/ENA for which the accession numbers are given [here](docs/data.md). This way, the dataset will still be available even if this S3 bucket cease to exist.  

## Dataset location

You can browser browse the gtgseq AWS S3 bucket by following [https://gtgseq.s3.amazonaws.com/index.html](https://gtgseq.s3.amazonaws.com/index.html) on your browser. Alternatively, you can use the aws cli:
```
aws s3 ls --no-sign-request s3://gtgseq/
```

There are three directories in the bucket and inside them you will find samples.
```
- ont-r10-5khz-dna
  |_ NA24385
  |_ NA24385_2
- ont-r10-dna
  |_ NA24385
  |_ NA12878
- ont-rna004-rna
  |_ UHR
```

`ont-r10-5khz-dna` contains data acquired with the latest 5KHz sampling rate, where as, `ont-r10-dna` contains legacy 4KHz sampling rate data. `ont-rna004-rna` contains direct-RNA data from RNA004.


## Structure

An example of the directory structure in the AWS S3 bucket is given below, for the sample ont-r10-dna/NA24385. The `raw` directory will contain the BLOW5 file and BLOW5 file index for random access. The `analyses` directory will contain data such as basecalls and modcalls. In this example, `basecalls` contain the default qscore passed high accuracy (hac) basecalls from Guppy 6.4.2 in bgzip compressed FASTQ format. FASTQ indexes (.fai and .gzi) are also available by accessing particular reads. Those reads aligned to the hg38 reference genome (without alternate contigs) using minimap2 2.14 is also available in BAM format. BAM index is also provided for region access. The `modcalls` contain the bgzip compressed CpG methylation frequencies from f5c 1.2. In the file names, guppy642hac refers to Guppy 6.4.2 hac,  mm217 refers to minimap2 2.17 and f5c12 refers to f5c 1.2.

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
  |         |_PGXX22394_guppy642hac.fastq.gz.fai
  |         |_PGXX22394_guppy642hac.fastq.gz.gzi
  |         |_PGXX22394_guppy642hac_mm217.bam
  |         |_PGXX22394_guppy642hac_mm217.bam.bai 
  |     |_modcalls
  |       |_f5c12
  |       |  |_PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz
  |       |_...
  |_......... 
  
```

Datasets and files are explained [here](docs/data.md) along with metadata.

Also, you will note that there is a `misc` directory directly in S3 bucket root. This directory contains miscellaneous stuff such as subsets and readID lists based on mapping coordiates for some of the above datasets. They are briefly documented [here](docs/misc.md).

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

# Direct Acesses

If can directly access https links using samtools (if compiled with curl support) for FASTQ and BAM; and, [slow5curl](https://github.com/BonsonW/slow5curl) for BLOW5. Please refer to the instructions [here](docs/slow5curl.md). 

#  Mounted Access

If you are doing your compute on AWS or if you have a very-high bandwidth and very-low latency Internet connection, you may mount the S3 bucket and then directly access as explained [here](docs/mount.md).

# Other public datasets

If you are interested in the previous nanopore chemistry R9.4.1, links to such data is available [here](https://github.com/hasindu2008/seq/#ont-r941-chemistry). 

# Acknowledgement

AWS Open Data Sponsorship Program for generously hosting this open data.
