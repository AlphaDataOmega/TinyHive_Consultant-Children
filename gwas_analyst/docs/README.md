# GWAS Analyst Documentation

## Overview

This directory contains reference documentation and standard operating procedures for the gwas_analyst consultant child agent.

## Domain Expertise

The gwas_analyst specializes in:

### Genotype Calling
- Illumina IDAT file processing
- GenomeStudio and crlmm clustering
- GenCall score quality assessment
- Call rate optimization

### Quality Control

#### Sample-Level QC
- Missingness filtering (1-2% threshold)
- Sex concordance via X-chromosome F-statistic
- Relatedness detection using PI-hat scores
- Population structure outlier removal
- Chromosomal abnormality detection

#### SNP-Level QC
- Call rate filtering (--geno)
- Minor allele frequency thresholds (--maf)
- Hardy-Weinberg equilibrium testing (--hwe, --hardy)
- Plate and batch effect assessment

### Error Detection
- Plate-level error identification
- Batch effect comparison
- Site-level handling differences
- Case/control processing bias detection
- Random error filtering via GenCall thresholds

### Population Stratification
- PCA analysis with Eigensoft smartpca
- STRUCTURE ancestry estimation
- Admixture population modeling
- Reference population integration (1000 Genomes)
- Outlier detection (>6 SD threshold)
- Appropriate eigenvector selection for adjustment

### Association Testing
- Case/control chi-squared analysis
- Logistic regression for binary traits
- Linear regression for quantitative traits
- Mixed models (GEMMA, BOLTLMM) for related samples
- Covariate adjustment strategies
- Multi-locus testing approaches

### Multiple Testing Correction
- Bonferroni correction
- Benjamini-Hochberg FDR
- Permutation testing
- Genome-wide significance thresholds

### Imputation
- Missing genotype imputation
- Full reference panel imputation
- Cross-platform data harmonization
- Imputation quality metrics

### Meta-Analysis
- Cross-study result combination
- Replication strategy design
- Linkage disequilibrium consideration
- Power calculation for study design

## Key Tools and Software

| Category | Tools |
|----------|-------|
| File Formats | PLINK binary (.bed, .bim, .fam) |
| QC & Analysis | PLINK, PLINK2 |
| Population Structure | Eigensoft (smartpca), STRUCTURE, Admixture |
| Mixed Models | GEMMA, BOLTLMM |
| Imputation | IMPUTE2, Minimac, Michigan Imputation Server |
| Reference Data | dbSNP, Ensembl, 1000 Genomes, HRC |
| Visualization | Manhattan plots, Q-Q plots, PCA scatter plots |
| Genotype Calling | GenomeStudio, crlmm |

## PLINK Command Reference

### Quality Control
```bash
# Sample missingness
plink --bfile input --mind 0.02 --make-bed --out output

# SNP missingness
plink --bfile input --geno 0.02 --make-bed --out output

# MAF filtering
plink --bfile input --maf 0.01 --make-bed --out output

# HWE filtering
plink --bfile input --hwe 1e-6 --make-bed --out output

# Sex check
plink --bfile input --check-sex --out output

# Relatedness
plink --bfile input --genome --out output
```

### Association Testing
```bash
# Basic association
plink --bfile input --assoc --out output

# Logistic regression
plink --bfile input --logistic --covar covars.txt --out output

# Linear regression
plink --bfile input --linear --covar covars.txt --out output
```

## Quality Control Thresholds

| Metric | Recommended Threshold |
|--------|----------------------|
| Sample missingness | 1-2% (--mind 0.01-0.02) |
| SNP missingness | 1-2% (--geno 0.01-0.02) |
| MAF | Study-specific (commonly 0.01-0.05) |
| HWE p-value | 1e-6 to 1e-10 |
| PI-hat relatedness | 0.18 (commonly used cutoff) |
| Sex F-statistic | F < 0.2 female, F > 0.8 male |
| PCA outliers | >6 standard deviations |
| GenCall minimum | >0.7 high quality, <0.2 failed |

## PI-hat Interpretation

| PI-hat Value | Interpretation |
|--------------|----------------|
| ~1.0 | Duplicate samples or MZ twins |
| >0.5 to <1.0 | Likely contamination |
| ~0.5 | Full siblings or parent-child |
| ~0.25 | Grandparent-grandchild or half-siblings |
| ~0.125 | First cousins |
| <0.0625 | Unrelated |

## Reference SOPs

Primary reference: `/home/ubuntu/TinyHive-sops/SOP_GWAS_Data_Processing.md`

Key workflow templates:
- Genotype calling pipeline
- Comprehensive QC workflow
- Population stratification assessment
- Association testing protocols
- Imputation pipeline
- Meta-analysis workflow
