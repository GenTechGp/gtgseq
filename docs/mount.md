# Directly processing on an s3fs mount

## Setting up s3fs mount

If you are doing your compute on AWS or if you have a very-high bandwidth and very-low latency Internet connection, given below is a trick to simply mounting the S3 bucket and then directly basecalling. This eliminates the need to download the BLOW5 file.

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


## Example: Basecalling a subset of reads without downloading the whole BLOW5

Assume you need to super accuracy basecall the reads belonging to the region chrX:147,910,000–147,950,000 without downloading a tera byte of data.
For this you will need [slow5tools](https://github.com/hasindu2008/slow5tools), [samtools](http://www.htslib.org/download/) and [buttery-eel](https://github.com/Psy-Fer/buttery-eel) installed.

```bash
# extract the list of read IDs that map to chrX:147,910,000–147,950,000 using samtools and bash commands
samtools view s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 chrX:147,910,000–147,950,000 | cut -f 1 | sort -u > read_ids.txt

# extract the raw reads from the BLOW5 file 
slow5tools get --list read_ids.txt s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 -o selected_reads.blow5

# basecall those selected reads
buttery-eel  -g /path/to/ont-guppy/bin/  --config dna_r9.4.1_450bps_sup.cfg --device 'cuda:all' -i selected_reads.blow5 -o  selected_reads.fastq --port 5555  --use_tcp
```

Note that slow5tools will load the index to the memory first which is around ~1GB. Then it will fetch requested records. 
If you have multiple regions, it is recommended that you batch all in to one list and invoke slow5tools once, so that the index is read/downloaded  only once.
Alternatively, you can manually download the index and create a symbolic link to the BLOW5 file as below:

```
# copy the index
cp s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5.idx ./PGXX22394_reads.blow5.idx

# create a symbolic link in the same directory
ln -s s3/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 ./PGXX22394_reads.blow5

# now use slow5tools get
slow5tools get --list read_ids.txt ./PGXX22394_reads.blow5 -o selected_reads.blow5
```


