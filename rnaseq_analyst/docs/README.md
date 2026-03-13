# RNA-Seq Analyst Documentation

This directory contains reference materials and standard operating procedures for RNA-Seq data processing and gene expression analysis.

## Overview

The RNA-Seq analyst specializes in transcriptomic analysis workflows including:

- **Quality Control**: FastQC, MultiQC for assessing sequencing data quality
- **Preprocessing**: Trimmomatic, Trim_Galore, BBMap for adapter and quality trimming
- **Alignment**: STAR, HISAT2 for splice-aware read alignment
- **Pseudo-alignment**: kallisto, Salmon for rapid transcript quantification
- **Count Generation**: featureCounts, HTSeq for gene-level counting
- **Statistical Analysis**: DESeq2, edgeR, limma for differential expression

## Workflow Summary

```
Raw FASTQ Files
       |
       v
PHASE 1: Preprocessing
- Quality check (FastQC)
- Adaptor/quality trimming
- Short read removal
- Quality recheck
       |
       v
PHASE 2: Count Generation
       |
       +---> Protocol 1: Alignment-Based
       |     - Splice-aware alignment (STAR/HISAT2)
       |     - Count generation (featureCounts)
       |     - Alignment stats collection
       |
       +---> Protocol 2: Pseudo-alignment
             - kallisto or Salmon
             - Estimated counts
       |
       v
PHASE 3: Statistical Analysis
- Import counts (tximport for pseudo-alignment)
- QC and outlier/batch detection
- Low count filtering and normalization
- Differential expression testing
       |
       v
Results and Visualization
```

## Key Tools Reference

### Quality Control
| Tool | Purpose |
|------|---------|
| FastQC | Quality assessment of raw reads |
| MultiQC | Aggregate QC reports across samples |

### Trimming and Filtering
| Tool | Purpose |
|------|---------|
| Trimmomatic | Adapter trimming, quality filtering, short read removal |
| Trim_Galore | Wrapper for Cutadapt and FastQC |
| BBMap | Suite of tools including BBDuk for preprocessing |

### Alignment
| Tool | Notes |
|------|-------|
| STAR | Ultrafast splice-aware aligner, auto-detects strandedness |
| HISAT2 | Low memory requirements, successor to TopHat |

### Pseudo-alignment
| Tool | Notes |
|------|-------|
| kallisto | kmer-based mapping to transcriptome |
| Salmon | Quasi-mapping with bias correction |

### Count Generation
| Tool | Notes |
|------|---------|
| featureCounts | Fast and efficient gene-level counting |
| HTSeq | Python-based counting tool |

### Statistical Analysis
| Package | Notes |
|---------|-------|
| DESeq2 | Negative binomial model, handles complex designs |
| edgeR | TMM normalization, robust differential expression |
| limma | Linear models, voom transformation for RNA-Seq |
| tximport | Import transcript-level estimates from kallisto/Salmon |

## Experimental Design Guidelines

- **Minimum Replicates**: 3 per condition (more preferred)
- **Read Depth**: 30-50 million reads for human samples
- **Trade-off**: Higher replicates (15-20M reads each) preferred over fewer samples with higher depth
- **Strandedness**: Verify library preparation method (standard dUTP is reverse-stranded)

## Quality Metrics

### Expected Alignment Rates
- Good quality human RNA-Seq: 70-90% alignment
- Below 60%: Evaluate parameters, check for contaminants

### Key Statistics to Track
- Total reads before/after trimming
- Uniquely mapped reads
- Multi-mapped reads
- Reads assigned to genes
- Unassigned reads (no feature, ambiguous)

## Normalization Methods

| Method | Package | Use Case |
|--------|---------|----------|
| CPM | Base | Simple depth normalization |
| TMM | edgeR | Accounts for composition bias |
| DESeq2 | DESeq2 | Median of ratios method |

## Multiple Testing Correction

All differential expression results should use FDR (False Discovery Rate) correction:
- Standard threshold: adjusted p-value < 0.05
- This means ~5% of significant genes may be false positives
- Threshold can be adjusted based on experimental goals

## Reproducibility Requirements

- Document all software versions
- Record all parameters used
- Maintain raw data as immutable
- Use version control for analysis scripts
- Consider Rmarkdown for reproducible reports
