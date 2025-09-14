
# Fetching subsets with slow5curl and samtools

If you intend on processing a specific subset of a remote BLOW5 file, slow5curl will let you fetch just this subset, without needing to download the whole thing locally. Using this tool is currently much more efficient than mounting an S3 bucket. Note that random access like this requires the necessary index files to reside in the remote directory next to their corresponding files. For a .blow5 this is the .blow5.idx, for a .bam file the .bam.bai, and for a bgzip compressed fastq.gz, the fastq.gz.gzi and fastq.gz.fai.

If you are looking to fetch multiple subsets from the same BLOW5 file, we recommend caching the index file locally to speed up the download. For more information: [slow5curl commands and options](https://bonsonw.github.io/slow5curl/commands.html).

## Installing necessary tools

Building [slow5curl](https://github.com/BonsonW/slow5curl) from the repo:

```bash
# install zlib and libcurl development libraries
sudo apt-get install zlib1g-dev libcurl4-openssl-dev
# clone and build from the repo
git clone --recursive https://github.com/BonsonW/slow5curl
cd slow5curl
make
```

Building [samtools](http://www.htslib.org/download/) from release:

```bash
wget https://github.com/samtools/samtools/releases/download/1.18/samtools-1.18.tar.bz2
tar -vxjf samtools-1.18.tar.bz2
cd samtools-1.18
./configure --prefix=/where/to/install   # make sure libcurl is installed on your system so that samtools build with curl enabled
make
make install
```

---

## Example: Fetching a subset of reads

Assume you want to get the raw signal reads from the genomic region chrX:147,910,000–147,950,000 without downloading a terabyte of data. You can use samtools to first grab the necessary read IDs from a remote BAM file and then slow5curl to fetch those reads from a remote BLOW5 file. Steps are as below:

```bash
# extract the list of read IDs that map to chrX:147,910,000–147,950,000 using samtools and bash commands
samtools view https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam chrX:147,910,000-147,950,000 | cut -f 1 | sort -u > read_ids.txt

# extract the raw reads from the BLOW5 file 
/path/to/slow5curl get --list read_ids.txt https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 -o selected_reads.blow5
```

If you want to fetch reads for multiple genomic regions, you can provide the list of coordinates in BED format to samtools:
```
samtools view https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam -L regions.bed -M | cut -f1 | sort -u > read_ids.txt 
```
Then you can provide this list to slow5curl to get all the necessary reads in one go.


## Example: Fetching and basecalling a subset of reads

Assume you need to super accuracy basecall the reads belonging to the region chrX:147,910,000–147,950,000 without downloading a terabyte of data. For this you will need [buttery-eel](https://github.com/Psy-Fer/buttery-eel) installed. Like before, we will need to extract the reads from the bam file and then fetch it.

```bash
# extract the list of read IDs that map to chrX:147,910,000–147,950,000 using samtools and bash commands
samtools view https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam chrX:147,910,000-147,950,000 | cut -f 1 | sort -u > read_ids.txt

# extract the raw reads from the BLOW5 file 
/path/to/slow5curl get --list read_ids.txt https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 -o selected_reads.blow5

# basecall those selected reads
buttery-eel -g /path/to/ont-guppy/bin/ --config dna_r9.4.1_450bps_sup.cfg --device 'cuda:all' -i selected_reads.blow5 -o  selected_reads.fastq --port 5555  --use_tcp
```

---

Please refer to the following publications for more details:

> Bonson Wong, James M Ferguson, Jessica Y Do, Hasindu Gamaarachchi, Ira W Deveson, Streamlining remote nanopore data access with slow5curl, GigaScience, Volume 13, 2024, giae016, https://doi.org/10.1093/gigascience/giae016
