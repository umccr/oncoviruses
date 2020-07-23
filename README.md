# 🦕 Oviraptor

![Build](https://github.com/vladsaveliev/oviraptor/workflows/CI/badge.svg) [![Anaconda-Server Badge](https://anaconda.org/vladsaveliev/oviraptor/badges/installer/conda.svg)](https://anaconda.org/vladsaveliev/oviraptor)

Detection of oncoviruses content and integration sites in cancer whole genome data

```
oviraptor tumor.bam -o results --host-fa hg38.fa
```

## Installation

Via conda:

```
conda install -c vladsaveliev oviraptor
```

Installing conda is optional if you have the following tools installed and available in $PATH:

- `python3`
- `minimap2`
- `samtools`
- `sambamba`
- `bcftools`
- `mosdepth`
- `snakemake`
- `lumpy` (on macOS, you can pull a dockerized version 
           with `docker pull quay.io/biocontainers/lumpy-sv:0.3.0--h0b85cd1_0`)
   
In this case you can install with:
   
```
git clone git@github.com:vladsaveliev/oviraptor.git
pip install oviraptor
```
   
## Usage

The tool requires:

 - a host whole genome seqeuncing BAM file as an input data (any human reference genome will work as the tool will extract reads from the file to realign), 
 - a human hg38 reference genome fasta file, which can be provided with `--host-fa` as follows:

```
oviraptor tumor.bam -o results --host-fa hg38.fa
```

The tool will also use a pre-packaged hg38 gene coordinates file to annotate the breakpoints. However you can override it with your own annotation file with `--host-gtf`, e.g.:

```
oviraptor tumor.bam -o results --host-fa hg38.fa --host-gtf Homo_sapiens.GRCh38.gtf.gz
```

If the `--host-fa` is not provided, the tool will attempt to download it from [AWS-iGenomes](https://github.com/ewels/AWS-iGenomes) using `awscli` into the output folder (`results/reference`, provided `-o results`), which might take a while and around 3G of space.

The tool can make use of multiple cores. To use 10 CPUs:

```
oviraptor tumor.bam -o results -t10
```

If you already know your candidate virus and just want to find the integration sites, use:

```
oviraptor tumor.bam -o results -v HPV18
```

If you don't need integration sites and just want to find viral content, use:

```
oviraptor tumor.bam -o results --only-detect
```

## Development

To develop, install with `-e` flag to pip:

```
git clone --recursive git@github.com:vladsaveliev/oviraptor.git
pip install -e oviraptor
```









