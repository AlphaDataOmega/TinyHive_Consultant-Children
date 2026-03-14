# Bioinformatics Workflow Specialist Documentation

## Overview

This directory contains reference documentation and standard operating procedures for the bioinformatics_workflow_specialist consultant child agent. This agent specializes in designing, implementing, and optimizing bioinformatics workflows for next-generation sequencing (NGS) data analysis.

## Domain Expertise

The bioinformatics_workflow_specialist covers comprehensive NGS analysis workflows:

### Pipeline Design and Architecture

#### Workflow Management Systems
| Platform | Best For | Key Features |
|----------|----------|--------------|
| Nextflow | Production pipelines | DSL2, containers, cloud-native |
| Snakemake | Python ecosystems | Conda integration, flexibility |
| WDL | GATK workflows | Cromwell engine, Terra platform |
| Galaxy | User-friendly analysis | GUI, reproducibility tracking |

#### Design Principles
- Modular architecture with discrete, reusable components
- Containerization using Docker and Singularity
- Version control for all scripts and configurations
- Checkpoint/restart functionality for fault tolerance
- Comprehensive logging and error handling

### 16S rRNA Microbiome Analysis

#### Workflow Phases
1. **Preprocessing**: Quality filtering, paired-end merging, chimera removal
2. **OTU/ASV Inference**: Clustering (97% identity) or exact ASV detection
3. **Taxonomic Classification**: Assignment against SILVA, GreenGenes, or RDP
4. **Diversity Analysis**: Alpha diversity, beta diversity, statistical testing

#### Key Tools
- **QIIME2**: Complete microbiome analysis platform
- **DADA2**: Exact ASV inference (R package)
- **mothur**: Alternative comprehensive pipeline
- **phyloseq**: R-based visualization and statistics
- **PEAR/PANDASeq**: Paired-end read merging
- **UCHIME/vsearch**: Chimera detection

### RNA-Seq Gene Expression Analysis

#### Alignment-Based Protocol
```
FASTQ -> Quality trim (Trimmomatic) -> Align (STAR/HISAT2) ->
  Count (featureCounts) -> Normalize (DESeq2/edgeR) ->
  Differential Expression -> Pathway Analysis
```

#### Pseudo-Alignment Protocol
```
FASTQ -> Quality trim -> Salmon/kallisto quantification ->
  tximport -> DESeq2/edgeR -> Differential Expression
```

#### Statistical Analysis Tools
| Tool | Normalization | Model | Best For |
|------|---------------|-------|----------|
| DESeq2 | Median of ratios | Negative binomial | Most cases |
| edgeR | TMM | Negative binomial | Large samples |
| limma-voom | TMM + voom | Linear model | Complex designs |

#### Quality Metrics
- Mapping rate: >70% for RNA-Seq
- Recommended coverage: 30-50M reads (human)
- Minimum replicates: 3 per condition

### Variant Calling Workflows

#### GATK Best Practices Pipeline
```
FASTQ -> BWA-MEM alignment -> Mark duplicates (Picard) ->
  BQSR (GATK) -> HaplotypeCaller -> VQSR/Hard filtering ->
  Annotation (VEP/ANNOVAR)
```

#### Functional Equivalence Standards
- Standardized tool versions
- Reference genome: GRCh38/GRCh37
- Known sites for recalibration (dbSNP, known indels)
- Target >98% VCF concordance between pipelines

#### Variant Callers
| Tool | Type | Best For |
|------|------|----------|
| GATK HaplotypeCaller | SNVs, indels | Germline variants |
| FreeBayes | SNVs, indels | Germline, flexible |
| Mutect2 | SNVs, indels | Somatic variants |
| DeepVariant | SNVs, indels | High accuracy |
| Strelka2 | SNVs, indels | Speed, somatic |

### GWAS Data Processing

#### Quality Control Checklist
**Sample-Level**
- Call rate >98%
- Sex concordance check
- Population structure verification (PCA)
- Relatedness filtering (PI-HAT)
- Heterozygosity outliers

**SNP-Level**
- Call rate >98%
- MAF threshold (typically >1%)
- Hardy-Weinberg equilibrium
- Batch effect detection

#### Association Analysis
- Population stratification: PCA, ADMIXTURE
- Single-locus testing: chi-squared, logistic/linear regression
- Mixed models: GEMMA, BOLT-LMM
- Multiple testing: Bonferroni, FDR correction

### Metagenomics Analysis

#### Workflow Components
1. Quality filtering and host removal
2. Metagenomic assembly (MetaSPAdes, MEGAHIT)
3. Contig binning (MetaBAT2, CONCOCT)
4. Bin quality assessment (CheckM)
5. Taxonomic classification (GTDB-Tk, Kraken2)
6. Functional annotation (Prokka, eggNOG-mapper)

### Quality Control Procedures

#### FastQC Metrics
| Metric | Passing | Action if Failed |
|--------|---------|------------------|
| Per base quality | >Q30 | Trim low-quality ends |
| Adapter content | <5% | Trim adapters |
| GC content | Expected distribution | Check contamination |
| Duplication | <50% (DNA) | Normal for RNA-Seq |

#### Alignment QC
| Metric | WGS Target | RNA-Seq Target |
|--------|------------|----------------|
| Mapping rate | >95% | >70% |
| Properly paired | >90% | >80% |
| Duplicate rate | <20% | Variable |

### Data Management

#### Directory Structure Standard
```
project/
├── raw_data/           # Immutable raw data
├── reference/          # Reference files
├── processed/          # Intermediate files
├── results/            # Final outputs
├── scripts/            # Analysis code
├── logs/               # Processing logs
└── docs/               # Documentation
```

#### NCBI Submission
- BioProject: Project metadata
- BioSample: Sample metadata
- SRA: Raw sequence data
- Aspera: High-speed data transfer

### HPC Environment

#### SLURM Resource Guidelines
| Analysis | CPUs | Memory | Time |
|----------|------|--------|------|
| FastQC | 4 | 4GB | 10 min |
| BWA-MEM (30X) | 16 | 32GB | 2 hours |
| STAR | 8 | 32GB | 30 min |
| HaplotypeCaller | 4 | 16GB | 4 hours |
| SPAdes | 16 | 64GB | 4-8 hours |

#### Module Management
```bash
module load bwa/0.7.17
module load samtools/1.15
module load gatk/4.3.0.0
```

## Key Tools Reference

### Quality Control
| Tool | Purpose |
|------|---------|
| FastQC | Read quality assessment |
| MultiQC | Aggregate QC reports |
| Picard | Alignment metrics |
| QUAST | Assembly quality |
| BUSCO | Completeness assessment |

### Preprocessing
| Tool | Purpose |
|------|---------|
| Trimmomatic | Adapter/quality trimming |
| BBDuk | Filtering, adapter removal |
| fastp | All-in-one preprocessing |
| cutadapt | Adapter trimming |

### Alignment
| Tool | Application |
|------|-------------|
| BWA-MEM | DNA alignment |
| STAR | RNA-Seq (splice-aware) |
| HISAT2 | RNA-Seq (splice-aware) |
| minimap2 | Long reads |
| Bowtie2 | Short reads |

### Quantification
| Tool | Application |
|------|-------------|
| featureCounts | Gene counts from BAM |
| HTSeq-count | Gene counts from BAM |
| Salmon | Pseudo-alignment quantification |
| kallisto | Pseudo-alignment quantification |

### Assembly
| Tool | Application |
|------|-------------|
| SPAdes | Bacterial genomes |
| Trinity | Transcriptome de novo |
| Flye | Long-read assembly |
| MEGAHIT | Metagenome assembly |
| MetaSPAdes | Metagenome assembly |

### Annotation
| Tool | Application |
|------|-------------|
| Prokka | Prokaryotic annotation |
| Funannotate | Fungal annotation |
| MAKER | Eukaryotic annotation |
| InterProScan | Functional domains |
| eggNOG-mapper | Functional annotation |

## Reference Databases

| Database | Purpose |
|----------|---------|
| NCBI RefSeq | Reference genomes |
| Ensembl | Genome annotation |
| SILVA | 16S/18S rRNA |
| GreenGenes | 16S taxonomy |
| UniProt | Protein sequences |
| dbSNP | Known variants |
| gnomAD | Population frequencies |
| ClinVar | Clinical significance |
| KEGG | Pathway annotation |
| GO | Gene ontology |

## File Formats

### Input Formats
- **FASTQ**: Raw sequencing reads with quality scores
- **FASTA**: Reference sequences
- **GTF/GFF**: Gene annotation
- **BED**: Genomic intervals

### Output Formats
- **BAM/CRAM**: Aligned reads
- **VCF**: Variant calls
- **BED**: Feature coordinates
- **TSV**: Count matrices

## Reproducibility

### Required Documentation
1. Software versions for all tools
2. Reference genome builds and annotation versions
3. Parameter settings for each step
4. Container/environment definitions
5. Script version control (Git)

### Environment Management
```yaml
# conda environment
name: ngs_pipeline
channels:
  - bioconda
  - conda-forge
dependencies:
  - bwa=0.7.17
  - samtools=1.15
  - gatk4=4.3.0.0
  - r-base=4.2
```

## Reference SOPs

Primary reference: `/home/ubuntu/TinyHive-sops/science/bioinformatics_workflow_sop.md`

Related SOPs:
- `/home/ubuntu/TinyHive-sops/bioinformatics_laboratory_sops.md`
- `/home/ubuntu/TinyHive-sops/SOP_RNA_Seq_Gene_Expression_Analysis.md`
- `/home/ubuntu/TinyHive-sops/SOP_GWAS_Data_Processing.md`
- `/home/ubuntu/TinyHive-sops/SOP_Fungal_Genome_Assembly_Complete_Guide.md`
- `/home/ubuntu/TinyHive-sops/SOP_16S_rRNA_Microbiome_Analysis.md`
- `/home/ubuntu/TinyHive-sops/healthcare_variant_calling_sop.md`

## Usage Examples

### Running a 16S Analysis
```bash
# QIIME2 workflow
qiime tools import --type 'SampleData[PairedEndSequencesWithQuality]' \
  --input-path manifest.tsv --output-path demux.qza

qiime dada2 denoise-paired --i-demultiplexed-seqs demux.qza \
  --p-trunc-len-f 240 --p-trunc-len-r 200 \
  --o-table table.qza --o-representative-sequences rep-seqs.qza
```

### Running RNA-Seq Alignment
```bash
# STAR alignment
STAR --runThreadN 8 --genomeDir star_index \
  --readFilesIn sample_R1.fq.gz sample_R2.fq.gz \
  --readFilesCommand zcat \
  --outSAMtype BAM SortedByCoordinate \
  --quantMode GeneCounts
```

### Running Variant Calling
```bash
# GATK HaplotypeCaller
gatk HaplotypeCaller \
  -R reference.fa \
  -I sample.bam \
  -O sample.g.vcf.gz \
  -ERC GVCF
```
