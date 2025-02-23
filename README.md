# 10X 2018 Data Repository

This repository contains code and data structure for importing and processing the **10X 2018 single-cell RNA sequencing data**. Here, we get **two similar single-cell RNA sequencing (scRNA-seq) experiments** conducted on **Human PBMC (Peripheral Blood Mononuclear Cells)** from a healthy donor. The datasets are provided by 10X Genomics as sample datasets. One dataset contains approximately 1000 cells, while the other contains approximately 10000 cells,

Data from the two experiments are labeled as:
- **pbmc_1k_v3** 
- **pbmc_10k_v3**

The pipeline includes downloading FASTQ files, preprocessing with **Cell Ranger**, and organizing processed data for downstream analysis.

---

## Directory Structure

After running the pipeline, the directory structure under the **`10X-2018`** directory is organized as follows:

```plaintext
10X-2018
├── raw
│   ├── pbmc_1k_v3_fastqs
│   │   ├── pbmc_1k_v3_S1_L001_R1_001.fastq
│   │   └── pbmc_1k_v3_S1_L001_R2_001.fastq
│   ├── pbmc_10k_v3_fastqs
│   │   ├── pbmc_10k_v3_S1_L001_R1_001.fastq
│   │   └── pbmc_10k_v3_S1_L001_R2_001.fastq
│   └── refdata-gex-GRCh38-2020-A
├── processed
│   ├── pbmc_1k_v3
│   │   ├── outs
│   │   │   ├── metrics_summary.csv
│   │   │   ├── filtered_feature_bc_matrix.h5
│   │   │   ├── molecule_info.h5
│   │   │   └── other_files...
│   ├── pbmc_10k_v3
│   │   ├── outs
│   │   │   ├── metrics_summary.csv
│   │   │   ├── filtered_feature_bc_matrix.h5
│   │   │   ├── molecule_info.h5
│   │   │   └── other_files...
```

---

## Pipeline Options

You can run the pipeline either in a single step or split into two steps:

### **Option 1: One-Step Execution**
To run the entire pipeline (downloading and processing) in one step, use:
```bash
qsub -l m_mem_free=64G integrated_pipeline.sh
```

### **Option 2: Two-Step Execution**
You can also run the pipeline in two separate steps:

#### **Step 1: Download Data**
```bash
qsub download_data.sh
```

#### **Step 2: Process Data**
After the data has been downloaded, process it with:
```bash
qsub -l m_mem_free=64G process_data.sh
```

---

## How to Run

1. **Clone the repository**:
   ```bash
   git clone git@github.com:Katsevich-Lab/import-10X-2018.git
   cd import-10X-2018
   ```

2. **Set up the environment**:
   Ensure `.research_config` contains the following:
   ```bash
   export LOCAL_10X_2018_DATA_DIR="/path/to/10X-2018/"
   ```

3. **Submit the job**:
   Use one of the pipeline options above to run the workflow.

---

## Notes

- Ensure all dependencies are installed and accessible in your `$PATH`:
  - `cellranger` and `wget`.
- Sufficient memory (≥64GB recommended) and disk space are required to process the data.

---

### **END** 

---