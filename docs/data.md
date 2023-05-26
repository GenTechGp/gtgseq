# ONT R10.4.1 chemistry - DNA data

## NA24385 (HG002) PromethION data (~30X)

- info: sheared DNA libraries (~17Kb) were prepared using the ONT LSK114 ligation library prep and a R10.4.1 flow cell was used to generate ~30X genome coverage.
- Notes: the complete dataset with 15.3M reads (102.2 Gbases). SRA: https://www.ncbi.nlm.nih.gov/sra/?term=SRS16575602
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-r10-dna/NA24385/

### raw signal data:
- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5  
  - s3 location: s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5
  - md5sum: `3498b595ac7c79a3d2dce47454095610`
- BLOW5 index
  - link: https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5.idx 
  - s3 location: s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5.idx
  - md5sum: `1e11735c10cf63edc4a7114f010cc472`
- Also available on SRA: [SRR23215366](https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR23215366&display=data-access) 

### basecalls:

- Guppy 6.4.2 high accuracy
  - basecalled with Guppy 6.4.2 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: dna_r10.4.1_e8.2_400bps_hac_prom.cfg
  - only reads that passed the qscore filter threshold 9 are included
    - FASTQ: [PGXX22394_guppy642hac.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.gz)
    - FASTQ index:  [PGXX22394_guppy642hac.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.gz.gzi) and [PGXX22394_guppy642hac.fastq.fai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.fai)
  - mapped with minimap2 2.17 against hg38noAlt with map-ont preset
    - BAM: [PGXX22394_guppy642hac_mm217.bam](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam)
    - BAM index: [PGXX22394_guppy642hac_mm217.bam.bai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam.bai)

### modcalls

- f5c 1.2 CpG methylation frequencies
  - PGXX22394_guppy642hac_mm217.bam and PGXX22394_guppy642hac.fastq.gz used as input 
  - bgzip compressed methylation freqencies: [PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/modcalls/f5c12/PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz)

## NA12878 (HG001) PromethION data (~30X)

- Notes:  the complete dataset with ~11M reads
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-r10-dna/NA12878/

### raw signal data:

- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5
  - s3 location: s3://gtgseq/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5
  - md5sum: `24266f6dabb8d679f7f520be6aa22694`
- BLOW5 index
  - direct link: https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5.idx
  - s3 location: s3://gtgseq/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5.idx
  - md5sum: `a5659f829b9410616391427b2526b853`

### basecalls:

- Guppy 6.4.2 high accuracy
  - basecalled with Guppy 6.4.2 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: dna_r10.4.1_e8.2_400bps_hac_prom.cfg
  - only reads that passed the qscore filter threshold 9 are included
    - FASTQ: [PGXXHX230142_guppy642hac.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac.fastq.gz)
    - FASTQ index:  [PGXXHX230142_guppy642hac.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac.fastq.gz.gzi) and [PGXXHX230142_guppy642hac.fastq.fai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac.fastq.fai)
  - mapped with minimap2 2.17 against hg38noAlt with map-ont preset
    - BAM: [PGXXHX230142_guppy642hac_mm217.bam](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac_mm217.bam)
    - BAM index: [PGXXHX230142_guppy642hac_mm217.bam.bai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac_mm217.bam.bai)

### modcalls

- f5c 1.2 CpG methylation frequencies
  - PGXX22394_guppy642hac_mm217.bam and PGXX22394_guppy642hac.fastq.gz used as input 
  - bgzip compressed methylation freqencies: [PGXXHX230142_guppy642hac_mm217_f5c12_mfreq.tsv.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/modcalls/f5c12/PGXXHX230142_guppy642hac_mm217_f5c12_mfreq.tsv.gz)
