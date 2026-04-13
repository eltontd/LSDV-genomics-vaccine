# LSDV-genomics-vaccine
NGS-based identification of pathogenic sequences and epitope prediction for lumpy skin disease subunit vaccine development
# LSDV-genomics-vaccine

## Objective
Identify strain-specific pathogenic sequences from lumpy skin disease virus (LSDV) field isolates using NGS data, and predict immunogenic epitopes for a subunit vaccine.

## Data
- **Sample size:** 15 clinical LSDV isolates (viral DNA extracted from skin nodules)
- **Sequencing:** Illumina MiSeq, 2x150 bp, ~10M reads per sample
- **Reference genome:** LSDV NC_003027

## Workflow Overview

1. **Quality control** – FastQC, MultiQC  
2. **Adapter trimming** – Trimmomatic (retained >92% reads)  
3. **Read alignment** – BWA-MEM to LSDV reference  
4. **Variant calling** – freebayes + iVar  
   - Identified **247 SNPs** and **12 indels**  
5. **Filtering** – Non-synonymous variants in envelope genes (GPCR, LSDV019, LSDV117) with population frequency >5%  
6. **Epitope prediction** – IEDB + NetMHC  
   - Selected **3 conserved surface-exposed epitopes** (MHC-I IC50 < 50 nM)

## Reproducibility

- `environment.yml` – Conda environment with all dependencies
- `scripts/` – Bash pipeline runner + R visualization script
- `results/` – Example output (variant table, coverage plot, epitope heatmap)

## How to run

```bash
# Clone repo
git clone https://github.com/yourusername/LSDV-genomics-vaccine.git
cd LSDV-genomics-vaccine

# Create Conda environment
conda env create -f environment.yml
conda activate lsdv_pipeline

# Run pipeline (example)
bash scripts/run_lsd_pipeline.sh -i data/raw_reads -r ref/LSDV_NC_003027.fasta
