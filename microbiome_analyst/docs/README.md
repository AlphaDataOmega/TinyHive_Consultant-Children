# Microbiome Analyst Documentation

This directory contains reference documentation and standard operating procedures for 16S rRNA microbiome analysis.

## Core Competencies

The Microbiome Analyst specializes in:

- **16S rRNA Gene Analysis**: Processing amplicon sequencing data from the 16S ribosomal RNA gene for bacterial and archaeal community profiling
- **OTU/ASV Analysis**: Both traditional 97% identity OTU clustering and modern ASV-based exact sequence variant approaches
- **Taxonomic Classification**: Assignment of taxonomic identity using multiple reference databases
- **Diversity Analysis**: Alpha (within-sample) and beta (between-sample) diversity metrics and statistics

## Workflow Overview

The standard 16S rRNA analysis pipeline consists of three main phases:

### Phase 1: Preprocessing of Reads
- Quality assessment (FASTQC, MultiQC)
- Trimming and filtering (Trimmomatic, PRINSEQ)
- Paired-end read stitching (PEAR, PANDASeq, FLASH)
- Chimera detection and removal (UCHIME)

### Phase 2: OTU/ASV Processing
- OTU picking (de novo, closed-reference, open-reference)
- ASV prediction with DADA2
- Taxonomic classification against SILVA, GreenGenes, or RDP
- Multiple sequence alignment (PyNAST, INFERNAL)
- Phylogenetic tree construction (FastTree)

### Phase 3: Diversity Analysis
- Alpha diversity metrics (Shannon, Chao1, observed species, PD whole tree)
- Beta diversity metrics (UniFrac, Bray-Curtis)
- Statistical testing (PERMANOVA, ANOSIM, Mantel tests)
- Visualization (PCoA, NMDS, heatmaps)

## Key Tools and Platforms

| Category | Tools |
|----------|-------|
| QC | FASTQC, MultiQC, PRINSEQ |
| Trimming | Trimmomatic, SolexaQA |
| Read Stitching | PEAR, PANDASeq, FLASH |
| Chimera Detection | UCHIME, ChimeraSlayer |
| OTU Clustering | UPARSE, vsearch, QIIME2 |
| ASV Analysis | DADA2 |
| Classification | RDP classifier, UCLUST, RTAX |
| Alignment | PyNAST, INFERNAL |
| Phylogeny | FastTree |
| Analysis Platforms | QIIME2, Mothur, phyloseq (R) |

## Reference Databases

| Database | Description |
|----------|-------------|
| SILVA | Comprehensive ribosomal RNA database |
| GreenGenes | 16S rRNA gene database |
| RDP | Ribosomal Database Project |

## Key Concepts

### OTU vs ASV
- **OTU (Operational Taxonomic Unit)**: Traditional approach clustering sequences at 97% identity threshold
- **ASV (Amplicon Sequence Variant)**: Modern approach using exact sequence variants for higher resolution

### Diversity Metrics
- **Alpha Diversity**: Diversity within a single sample (richness, evenness)
- **Beta Diversity**: Diversity between samples (community dissimilarity)
- **UniFrac**: Phylogenetic distance metric incorporating evolutionary relationships

### Quality Considerations
- Minimum Phred quality score: Q3 (per Bokulich et al. 2013)
- Rarefaction required before diversity comparisons
- Chimera detection essential for accurate community profiling

## Related SOPs

- SOP_16S_rRNA_Microbiome_Analysis.md - Complete standard operating procedure for 16S rRNA data processing
