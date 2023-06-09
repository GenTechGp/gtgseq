# Directly processing on an s3fs mount

## Setting up s3fs mount

If you are doing your compute on AWS or if you have a very-high bandwidth and very-low latency Internet connection, given below is a method to simply mounting the S3 bucket and then directly basecalling. This eliminates the need to download the BLOW5 file. A more efficient method that directly uses the s3 API for BLWO5 is planned to be developed.

First install s3fs and then mount the s3 public bucket:

```bash
# install s3fs first
sudo apt-get install s3fs
# directory to mount the bucket
mkdir ./s3
# command to mount the public bucket gtgseq onto ./s3 directory
s3fs gtgseq ./s3/ -o public_bucket=1  -o url=http://s3.amazonaws.com/ -o dbglevel=info -o curldbg -o umask=0005 -o  uid=$(id -u)
```

Verify if the bucket is properly mounted by listing contents:
```bash
$ls ./s3/
index.html  ont-r10-dna
...
```

Now simply do the analysis you want on this file. For example, let us skim through a blow5 file
```
slow5tools skim s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 | head
```

At the end, you can umount usingthe following command:

```bash
fusermount -u ./s3
```

---

## Example: Basecalling on a full sample

To directly basecall a S/BLOW5 file, install [buttery-eel](https://github.com/Psy-Fer/buttery-eel), the S/BLOW5 basecaller wrapper for ONT Guppy, as instructed in the buttery-eel readme. Now simply point to a BLOW5 file in the mounted s3 bucket, for example:

``` bash
# source the buttery-eel virtual environment if you haven't already done so
source ./venv3/bin/activate

# running buttery-eel
buttery-eel  -g /path/to/ont-guppy/bin/  --config dna_r9.4.1_450bps_hac.cfg --device 'cuda:all' -i s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 -o  reads.fastq --port 5555  --use_tcp
```

Make sure you invoke `watch -n0 nvidia-smi` and monitor the GPU utilisation for a while to verify if there are not too many gaps with a 0% utilisation. Such gaps mean that your GPUs can process much faster than what your internet connection can server, thus you are better off downloading the BLOW5 to a local drive first.

## Example: Basecalling a subset of reads without downloading the whole BLOW5

Assume you need to super accuracy basecall the reads belonging to the region chrX:147,910,000–147,950,000 without downloading a tera byte of data.
For this you will need [slow5tools](https://github.com/hasindu2008/slow5tools), [samtools](http://www.htslib.org/download/) and [buttery-eel](https://github.com/Psy-Fer/buttery-eel) installed.

```bash
# extract the list of read IDs that map to chrX:147,910,000–147,950,000 using samtools and bash commands
samtools view s3/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam chrX:147,910,000-147,950,000 | cut -f 1 | sort -u > read_ids.txt

# extract the raw reads from the BLOW5 file 
slow5tools get --list read_ids.txt s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 -o selected_reads.blow5

# basecall those selected reads
buttery-eel  -g /path/to/ont-guppy/bin/  --config dna_r9.4.1_450bps_sup.cfg --device 'cuda:all' -i selected_reads.blow5 -o  selected_reads.fastq --port 5555  --use_tcp
```

On a system connected to Internet with a 1 Gbps connection at Garvan Institute, it took ~10s for samtools and slow5tools get took ~5 minutes. This is opposed to to ~3 hours that would have been required to download the whole ~1TB dataset.

Note that slow5tools will load the index to the memory first which is around ~1GB. Then it will fetch requested records. 
If you have multiple regions, it is recommended that you batch all in to one list and invoke slow5tools once, so that the index is read/downloaded  only once.
Alternatively, you can manually download the index and create a symbolic link to the BLOW5 file and then use slow5tools get as many times as you like.

```
# copy the index
cp s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5.idx ./PGXX22394_reads.blow5.idx

# create a symbolic link in the same directory
ln -s s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 ./PGXX22394_reads.blow5

# now use slow5tools get
slow5tools get --list read_ids.txt ./PGXX22394_reads.blow5 -o selected_reads.blow5
```

The ~5 minutes for slow5tools get above, now dropped to ~4 minutes. 

Note that s3fs is not very efficient, but this is proof of concept how partial downloads are possible with BLOW5. Using the S3 API will make it much faster, which we expect to do in future.

Likewise, if you want to fetch a batch of reads from an existing fastq.gz file, you can use a similar apprach with samtools:
```
samtools faidx -r read_ids.txt s3/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.gz > selected_reads.fastq
```
Took around 4.5 mins on the same system mentioned above.

Note that random access like this requires the necessary index files to reside on the S3 bucket next to their correspnding files. For a .blow5 this is the .blow5.idx, for a .bam file the .bam.bai, and for a bgzip compressed fastq.gz, the fastq.gz.gzi and fastq.gz.fai.

