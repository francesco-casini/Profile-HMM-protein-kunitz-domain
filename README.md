# Profile Hidden Markov Model for Kunitz Domain Prediction

This project was developed as part of the **Laboratory of Bioinformatics 1** course (Academic year 2023-2024)for the Master’s Degree in Bioinformatics at the **University of Bologna**.

The work focuses on the precise identification and characterization of the **Kunitz-type protease inhibitor domain**, a structurally conserved motif present in proteins that inhibit proteolytic enzymes.

## Project Description

The  objective of this project was to develop a **Profile Hidden Markov Model (HMM)** functioning as a binary classifier to detect the presence of **Kunitz domains** in protein sequences.

### Biological Context

Kunitz domains:

* Are small domains (~60 amino acids)
* Exhibit a conserved fold
* Are stabilized by *hree disulfide bonds (six conserved cysteines)
* Appear across diverse taxa
* Perform varied biological functions:

  * Inflammatory regulation in vertebrates
  * Anticoagulation in arthropods
  * Protease inhibition across multiple lineages

Despite structural conservation, functional and evolutionary variability makes computational detection non-trivial.


## Data and Methodology

A rigorous and reproducible computational pipeline was implemented to ensure model robustness.

### 1. Structural Data Selection

High-quality structural templates were retrieved from the **RCSB-PDB** database using strict criteria:

* High-resolution diffraction structures
* Appropriate sequence length
* Confirmed Kunitz fold


### 2. Model Construction

* A multiple structure alignment was performed using **PDBeFold**
* The structure-guided alignment was converted into a **multiple sequence alignment (MSA)**
* The MSA served as input for HMM construction using **PyHMMER**

The use of structural alignment ensured conservation of functionally critical residues, particularly the six cysteines responsible for disulfide bond formation.


### 3. Benchmarking Dataset

To evaluate model performance:

* Positive and negative benchmark sets were retrieved from **UniProt/Swiss-Prot**
* Dataset redundancy and bias were reduced using **BLAST**

  * Sequences highly similar to training data were filtered out
  * Ensured strict separation between training and testing data

### 4. Model Optimization

* 70% of the dataset used for model tuning
* 2-fold cross-validation
* Systematic evaluation of multiple E-value thresholds
* Optimal threshold selected by maximizing the **Matthews Correlation Coefficient (MCC)**

MCC was chosen as the primary metric due to its robustness in imbalanced binary classification settings.


## Results

The final evaluation on the independent test set demonstrated near-perfect performance:

* **Accuracy:** 0.999
* **Matthews Correlation Coefficient (MCC):** 0.995

A sequence previously reported as a “false positive” (UniProt ID: P56409) was manually investigated and confirmed to be a true Kunitz domain that had been overlooked in traditional annotations.

This result underscores:

* The discriminative power of structure-informed HMM profiles
* The model’s potential utility in refining biological database annotations


## Technical Implementation

The project is implemented in **Python** and integrates the following specialized tools:


* **RCSB-PDB API**
  Automated retrieval of high-quality structural templates

* **BLAST**
  Redundancy filtering and dataset curation
  
* **PDBeFold**
  Structure-based multiple alignment

* **Skylign**
  Generation of sequence logos to visualize conserved residues

* **PyHMMER**
  Profile HMM construction, searching and statistical evaluation

## Conclusion

This project demonstrates that structure-guided Profile HMMs provide highly accurate detection of Kunitz domains and can outperform traditional annotation pipelines. The results highlight the importance of combining structural biology and probabilistic modeling for precise domain prediction in protein sequences.
