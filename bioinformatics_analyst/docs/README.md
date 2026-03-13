# Bioinformatics Analyst Documentation

## Overview

This directory contains reference documentation and standard operating procedures for the bioinformatics_analyst consultant child agent.

## Domain Expertise

The bioinformatics_analyst specializes in:

### Genome Assembly and Annotation
- Funannotate pipeline for fungal genome annotation
- RepeatModeler/RepeatMasker for repeat identification
- PASA with MySQL/MariaDB for gene structure annotation
- Augustus configuration and training

### Metagenomics Analysis
- BBTools suite (BBDuk, BBNorm, BBMerge) for preprocessing
- SPAdes/MetaSPAdes for assembly
- CheckM for assembly quality assessment
- GTDB-TK for taxonomic classification
- AutoMeta for contig binning

### Amplicon Analysis
- AMPtk pipeline for 16S/ITS processing
- OTU clustering and taxonomy assignment
- FUNGuild functional guild analysis

### Phylogenomics
- PHYling for species tree construction
- Marker sets: AFTOL, BUSCO/OrthoDB, JGI single-copy genes
- HMMer, TrimAl, and muscle for sequence alignment

### Transcriptomics
- Trinity de novo and genome-guided assembly
- TransDecoder for protein inference
- Strand-specific RNA-seq handling

### Contamination Assessment
- BlobTools2 for contamination visualization
- Diamond and BLAST taxonomic screening
- Coverage-based filtering

### Data Management
- NCBI submission workflows (BioProject, BioSample, SRA)
- Aspera for high-speed data transfer
- HPCC data organization best practices

### Visualization
- JBrowse genome browser configuration
- CLINKER synteny graphics
- BiG-SCAPE secondary metabolite visualization

## Key Tools and Software

| Category | Tools |
|----------|-------|
| Assembly | SPAdes, MetaSPAdes, Trinity |
| Annotation | Funannotate, PASA, antiSMASH |
| Quality | FastQC, BUSCO, QUAST, CheckM |
| Alignment | BWA, Samtools, BLAST, Diamond |
| Taxonomy | GTDB-TK, mmseqs2, KronaTools |
| Amplicon | AMPtk, dada2 |
| Phylogenomics | PHYling, IQ-TREE, phytools |
| Visualization | JBrowse, CLINKER, BiG-SCAPE |
| Data Transfer | SRA Toolkit, Aspera |

## HPC Environment

Designed for SLURM-based HPC clusters with:
- Module-based software management
- Job array processing for batch workflows
- Scratch space for temporary files
- Shared data directories with immutable raw data

## Reference SOPs

Primary reference: `/home/ubuntu/TinyHive-sops/bioinformatics_laboratory_sops.md`

Key workflow templates:
- Funannotate annotation pipeline
- AMPtk amplicon processing
- Metagenomics assembly workflow
- PHYling phylogenomic analysis
- BlobTools contamination assessment
- JBrowse configuration
