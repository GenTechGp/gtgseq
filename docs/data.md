# ONT R10.4.1 5kHz chemistry - DNA data

Make sure to first go through the directory structure, file name conventions and downloading method documented [here](../README.md).

## Table of Contents
- [ONT R10.4.1 5kHz chemistry - DNA data](#ont-r1041-5khz-chemistry---dna-data)
  - [NA24385 (HG002) PromethION data (~40X)](#na24385-hg002-promethion-data-40x)
  - [NA24385 (HG002) PromethION data (~20X)](#na24385-hg002-promethion-data-20x)
- [ONT RNA004 chemistry - RNA data](#ont-rna004-chemistry---rna-data)
  - [UHR PromethION data](#uhr-promethion-data)
- [ONT R10.4.1 4kHz chemistry - DNA data](#ont-r1041-5khz-chemistry---dna-data)
  - [NA24385 (HG002) PromethION data (~30X)](#na24385-hg002-promethion-data-30x)
  - [NA12878 (HG001) PromethION data (~20X)](#na12878-hg001-promethion-data-20x)


## NA24385 (HG002) PromethION data (~40X)

- Info: HG002 (Coriell Institute, GM24385) was cultured in RPMI1640 (Gibco, 11875093) with 15% fetal bovine serum (Bovogen, SFBS-AU) at 37°C with 5% CO2. DNA was extracted using Nanobind CBB kit (PacBio, 102-301-900). DNA was sheared to ~33 kb using the Megaruptor 3 (Diagenode) and libraries prepared using SQK-LSK114 and sequenced on a R10.4.1 flow cell (Oxford Nanopore Technologies) at 5kHz sampling rate to generate ~40X genome coverage.
- Notes: the complete dataset with 18.8M reads (130.494 Gbases).
- Reads lengths: 2.7 kbases median, 6.9 kbases mean, 854.8 kbases max
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-r10-5khz-dna/NA24385_2/

### raw signal data:
- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: [PGXXSX240041_reads.blow5](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/raw/PGXXSX240041_reads.blow5)  
  - s3 location: s3://gtgseq/ont-r10-5khz-dna/NA24385_2/raw/PGXXSX240041_reads.blow5
  - md5sum: `b9e0f4fc49ffe4d1e39dc9c09eccdeac`
- BLOW5 index
  - direct link: [PGXXSX240041_reads.blow5.idx](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/raw/PGXXSX240041_reads.blow5.idx) 
  - s3 location: s3://gtgseq/ont-r10-5khz-dna/NA24385_2/raw/PGXXSX240041_reads.blow5.idx
  - md5sum: `18ac205e53552bcb561ea5b3a55cd9b7`

### basecalls:

- Guppy 6.5.7 high accuracy
  - basecalled with Guppy 6.5.7 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: dna_r10.4.1_e8.2_400bps_5khz_hac_prom.cfg
  - only reads that passed the qscore filter threshold 9 are included
    - FASTQ: [PGXXSX240041_guppy657hac.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/analyses/basecalls/guppy657hac/PGXXSX240041_guppy657hac.fastq.gz)
    - FASTQ index:  [PGXXSX240041_guppy657hac.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/analyses/basecalls/guppy657hac/PGXXSX240041_guppy657hac.fastq.gz.gzi) and [PGXXSX240041_guppy657hac.fastq.gz.fai](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/analyses/basecalls/guppy657hac/PGXXSX240041_guppy657hac.fastq.gz.fai)
  - mapped with minimap2 2.26 against hg38noAlt with map-ont preset
    - BAM: [PGXXSX240041_guppy657hac_mm226.bam](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/analyses/basecalls/guppy657hac/PGXXSX240041_guppy657hac_mm226.bam)
    - BAM index: [PGXXSX240041_guppy657hac_mm226.bam.bai](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/analyses/basecalls/guppy657hac/PGXXSX240041_guppy657hac_mm226.bam.bai)

### modcalls

- f5c 1.3 CpG methylation frequencies
  - PGXXSX240041_guppy657hac_mm226.bam and PGXXSX240041_guppy657hac.fastq.gz used as input 
  - bgzip compressed methylation freqencies: [PGXXSX240041_guppy657hac_mm226_f5c13_mfreq.tsv.gz](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385_2/analyses/modcalls/f5c13/PGXXSX240041_guppy657hac_mm226_f5c13_mfreq.tsv.gz)


## NA24385 (HG002) PromethION data (~20X)

- Info: sheared DNA libraries (~25Kb) were prepared using the ONT LSK114 ligation library prep and a R10.4.1 flow cell at 5kHz sampling rate was used to generate ~20X genome coverage.
- Notes: the complete dataset with 12.5M reads (51.211 Gbases).
- Reads lengths: 1.5 kbases median, 4.1 kbases mean, 288.9 kbases max
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-r10-5khz-dna/NA24385/

### raw signal data:
- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: [PGXXXX230339_reads.blow5](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/raw/PGXXXX230339_reads.blow5)  
  - s3 location: s3://gtgseq/ont-r10-5khz-dna/NA24385/raw/PGXXXX230339_reads.blow5
  - md5sum: `2dab2e0c042b0fb5f9f3794c7c916420`
- BLOW5 index
  - direct link: [PGXXXX230339_reads.blow5.idx](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/raw/PGXXXX230339_reads.blow5.idx) 
  - s3 location: s3://gtgseq/ont-r10-5khz-dna/NA24385/raw/PGXXXX230339_reads.blow5.idx
  - md5sum: `84a1b5317f0e92f73143070481df8fe3`

### basecalls:

- Guppy 6.5.7 high accuracy
  - basecalled with Guppy 6.5.7 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: dna_r10.4.1_e8.2_400bps_5khz_hac_prom.cfg
  - only reads that passed the qscore filter threshold 9 are included
    - FASTQ: [PGXXXX230339_guppy657hac.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/analyses/basecalls/guppy657hac/PGXXXX230339_guppy657hac.fastq.gz)
    - FASTQ index:  [PGXXXX230339_guppy657hac.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/analyses/basecalls/guppy657hac/PGXXXX230339_guppy657hac.fastq.gz.gzi) and [PGXXXX230339_guppy657hac.fastq.gz.fai](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/analyses/basecalls/guppy657hac/PGXXXX230339_guppy657hac.fastq.gz.fai)
  - mapped with minimap2 2.26 against hg38noAlt with map-ont preset
    - BAM: [PGXXXX230339_guppy657hac_mm226.bam](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/analyses/basecalls/guppy657hac/PGXXXX230339_guppy657hac_mm226.bam)
    - BAM index: [PGXXXX230339_guppy657hac_mm226.bam.bai](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/analyses/basecalls/guppy657hac/PGXXXX230339_guppy657hac_mm226.bam.bai)

### modcalls

- f5c 1.3 CpG methylation frequencies
  - PGXXXX230339_guppy657hac_mm226.bam and PGXXXX230339_guppy657hac.fastq.gz used as input 
  - bgzip compressed methylation freqencies: [PGXXXX230339_guppy657hac_mm226_f5c13_mfreq.tsv.gz](https://gtgseq.s3.amazonaws.com/ont-r10-5khz-dna/NA24385/analyses/modcalls/f5c13/PGXXXX230339_guppy657hac_mm226_f5c13_mfreq.tsv.gz)

# ONT RNA004 chemistry - RNA data

## UHR PromethION data 

- Info: Universal human reference RNA (300 ng polyA enriched RNA) was prepared using the SQK-RNA004 kit from Nanopore. Prepared library (48 ng) was loaded onto a FLO-PRO004RA flow cell.
- Notes: the complete dataset with 15.4M reads (17.554 Gbases).
- Reads lengths: 864 bases median, 1.137 kbases mean, 321 kbases max
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-rna004-rna/UHR/

### raw signal data:
- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: [PNXRXX240011_reads.blow5](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/raw/PNXRXX240011_reads.blow5)  
  - s3 location: s3://gtgseq/ont-rna004-rna/UHR/raw/PNXRXX240011_reads.blow5
  - md5sum: `671be5b88f2b54a9e22ced351493b7a9`
- BLOW5 index
  - direct link: [PNXRXX240011_reads.blow5.idx](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/raw/PNXRXX240011_reads.blow5.idx) 
  - s3 location: s3://gtgseq/ont-rna004-rna/UHR/raw/PNXRXX240011_reads.blow5.idx
  - md5sum: `e3ea326d300a22008e2821ce10d17649`

### basecalls:

- Dorado server 7.2.13 super accuracy
  - basecalled with Dorado server 7.2.13 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: rna_rp4_130bps_sup.cfg
  - only reads that passed the qscore filter threshold 10 are included
    - FASTQ: [PNXRXX240011_dorado7213sup.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/analyses/basecalls/dorado7213sup/PNXRXX240011_dorado7213sup.fastq.gz)
    - FASTQ index:  [PNXRXX240011_dorado7213sup.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/analyses/basecalls/dorado7213sup/PNXRXX240011_dorado7213sup.fastq.gz.gzi) and [PNXRXX240011_dorado7213sup.fastq.gz.fai](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/analyses/basecalls/dorado7213sup/PNXRXX240011_dorado7213sup.fastq.gz.fai)
  - mapped with minimap2 2.26 against gencode.v40.transcripts with map-ont preset and `-uf` 
    - BAM: [PNXRXX240011_dorado7213sup_mm226.bam](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/analyses/basecalls/dorado7213sup/PNXRXX240011_dorado7213sup_mm226.bam)
    - BAM index: [PNXRXX240011_dorado7213sup_mm226.bam.bai](https://gtgseq.s3.amazonaws.com/ont-rna004-rna/UHR/analyses/basecalls/dorado7213sup/PNXRXX240011_dorado7213sup_mm226.bam.bai)

# ONT R10.4.1 4kHz chemistry - DNA data

## NA24385 (HG002) PromethION data (~30X)

- Info: sheared DNA libraries (~17Kb) were prepared using the ONT LSK114 ligation library prep and a R10.4.1 flow cell at 4KHz sampling rate was used to generate ~30X genome coverage.
- Notes: the complete dataset with 15.3M reads (102.2 Gbases). Also available on SRA: [SRS16575602](https://www.ncbi.nlm.nih.gov/sra/?term=SRS16575602).
- Reads lengths: 6.5 kbases median, 7.3 kbases mean, 636.6 kbases max
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-r10-dna/NA24385/

### raw signal data:
- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: [PGXX22394_reads.blow5](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5)  
  - s3 location: s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5
  - md5sum: `3498b595ac7c79a3d2dce47454095610`
- BLOW5 index
  - direct link: [PGXX22394_reads.blow5.idx](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5.idx) 
  - s3 location: s3://gtgseq/ont-r10-dna/NA24385/raw/PGXX22394_reads.blow5.idx
  - md5sum: `1e11735c10cf63edc4a7114f010cc472`
- Also available on SRA: [SRR23215366](https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR23215366&display=data-access)
- Also available on ENA: [ERR11777845](https://www.ebi.ac.uk/ena/browser/view/ERR11777845) 

### basecalls:

- Guppy 6.4.2 high accuracy
  - basecalled with Guppy 6.4.2 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: dna_r10.4.1_e8.2_400bps_hac_prom.cfg
  - only reads that passed the qscore filter threshold 9 are included
    - FASTQ: [PGXX22394_guppy642hac.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.gz)
    - FASTQ index:  [PGXX22394_guppy642hac.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.gz.gzi) and [PGXX22394_guppy642hac.fastq.gz.fai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac.fastq.gz.fai)
  - mapped with minimap2 2.17 against hg38noAlt with map-ont preset
    - BAM: [PGXX22394_guppy642hac_mm217.bam](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam)
    - BAM index: [PGXX22394_guppy642hac_mm217.bam.bai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/basecalls/guppy642hac/PGXX22394_guppy642hac_mm217.bam.bai)

### modcalls

- f5c 1.2 CpG methylation frequencies
  - PGXX22394_guppy642hac_mm217.bam and PGXX22394_guppy642hac.fastq.gz used as input 
  - bgzip compressed methylation frequencies: [PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA24385/analyses/modcalls/f5c12/PGXX22394_guppy642hac_mm217_f5c12_mfreq.tsv.gz)

## NA12878 (HG001) PromethION data (~20X)

- Info: Sheared DNA libraries (~30Kb) were prepared using the ONT LSK114 ligation library prep and a R10.4.1 flow cell at 4KHz sampling rate was used to generate ~30X genome coverage.
- Notes:  the complete dataset with ~11M reads (70.5 Gbases)
- Reads lengths: 4.5 kbases median, 7.6 kbases mean, 235.1 kbases max
- Browse: https://gtgseq.s3.amazonaws.com/index.html#ont-r10-dna/NA12878/

### raw signal data:

- [BLOW5](https://www.nature.com/articles/s41587-021-01147-4) file 
  - direct link: [PGXXHX230142_reads.blow5](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5)
  - s3 location: s3://gtgseq/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5
  - md5sum: `24266f6dabb8d679f7f520be6aa22694`
- BLOW5 index
  - direct link: [PGXXHX230142_reads.blow5.idx](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5.idx)
  - s3 location: s3://gtgseq/ont-r10-dna/NA12878/raw/PGXXHX230142_reads.blow5.idx
  - md5sum: `a5659f829b9410616391427b2526b853`
- Also available on ENA: [ERR11777844](https://www.ebi.ac.uk/ena/browser/view/ERR11777844) 

### basecalls:

- Guppy 6.4.2 high accuracy
  - basecalled with Guppy 6.4.2 through [buttery-eel](https://github.com/Psy-Fer/buttery-eel). 
  - model: dna_r10.4.1_e8.2_400bps_hac_prom.cfg
  - only reads that passed the qscore filter threshold 9 are included
    - FASTQ: [PGXXHX230142_guppy642hac.fastq.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac.fastq.gz)
    - FASTQ index:  [PGXXHX230142_guppy642hac.fastq.gz.gzi](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac.fastq.gz.gzi) and [PGXXHX230142_guppy642hac.fastq.gz.fai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac.fastq.gz.fai)
  - mapped with minimap2 2.17 against hg38noAlt with map-ont preset
    - BAM: [PGXXHX230142_guppy642hac_mm217.bam](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac_mm217.bam)
    - BAM index: [PGXXHX230142_guppy642hac_mm217.bam.bai](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/basecalls/guppy642hac/PGXXHX230142_guppy642hac_mm217.bam.bai)

### modcalls

- f5c 1.2 CpG methylation frequencies
  - PGXXHX230142_guppy642hac_mm217.bam and PGXXHX230142_guppy642hac.fastq.gz used as input 
  - bgzip compressed methylation freqencies: [PGXXHX230142_guppy642hac_mm217_f5c12_mfreq.tsv.gz](https://gtgseq.s3.amazonaws.com/ont-r10-dna/NA12878/analyses/modcalls/f5c12/PGXXHX230142_guppy642hac_mm217_f5c12_mfreq.tsv.gz)
