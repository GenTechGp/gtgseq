# Open Data from Genomic Technologies Group

You can browser browse the gtgseq AWS S3 bucket by following [https://gtgseq.s3.amazonaws.com/index.html](https://gtgseq.s3.amazonaws.com/index.html) on your broswer. Alternatively, you can use the aws cli:
```
aws s3 ls s3://gtgseq/
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
  |     |_methcalls
  |_......... 
  
- pb-revio
  ....
```

Downloading a file can be done using the web browser; a CLI tool such as wget, curl or axel; or, aws cli. Downloading through aws cli is faster and recommeneded, especially for larger files.

Example using wget:
```
wget https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5
```

Example using aws cli:
```
aws s3 cp --no-sign-request s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5 ./
```

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

# Acknowledgement

AWS Open Data Sponsorship Program for generously hosting this open data.
