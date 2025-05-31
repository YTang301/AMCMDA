# AMCMDA

This repository provides the implementation of our manuscript:

> **"Identifying potential miRNA-disease associations through an accurate matrix completion approach"**  
> *(Submitted to Briefings in Bioinformatics, 2025)*

This repository enables reproducible prediction of potential miRNA–disease associations, and outputs all results in a structured `.xlsx` file.


##  Overview

AMCMDA integrates similarity fusion, truncated nuclear norm and ADMM to construct an effective predictor for identifying miRNA–disease associations.



##  How to Run

1. **Install Python dependencies**:
   numpy==1.26.4
   pandas==1.4.2
   openpyxl==3.0.9
   

2. **Run**:
AMCMDA.ipynb
To open and run a Jupyter Notebook, follow these steps:
(1) Install Jupyter (if not already installed): pip install notebook
(2) Launch Jupyter Notebook:
In your terminal or command prompt, run: jupyter notebook
(3) Open the Notebook:
Your default web browser will open with the Jupyter dashboard. Navigate to the desired notebook file () and click to open.
(4) Run Cells:
Click on a code cell and press  to run it. Alternatively, use the "Run" button in the toolbar.


3. **Output**:
   - `AMCMDA_Case_Study_Results.xlsx` — includes the predicted score for each `(disease, miRNA)` pair, with headers:
     
     Disease | miRNA | Score | Label

4.**Function**:

(1) Data Loading Functions
This project provides utility functions to load microRNA-disease association datasets from different HMDD versions (v1.0, v2.0, and v3.2).

(i) load_file(file_path, dtype=int, delimiter=None)
Loads data from Excel (.xlsx) or text (.txt) files.
Returns a pandas DataFrame for Excel files and a NumPy array for text files.
(ii) create_interaction_matrix(MDA, nd, nm)
Converts microRNA-disease association pairs into a binary interaction matrix of shape (nd, nm).
(iii) load_microRNA_disease_dataset(version='v1.0')
Loads the full dataset corresponding to the specified HMDD version.
The function itself defaults to call the dataset HMDD v1.0, if you want to call other datasets you need to write the dataset version in the parentheses of the function. For example, if you want to call the HMDD v2.0 dataset you should write 'v2.0' in the parentheses.

(2) AMCMDA Functions
This module implements the AMC algorithm for microRNA-disease association prediction, including matrix completion via singular value thresholding.

(i) singular_value_thresholding(Y, b)
Applies Singular Value Thresholding (SVT) to matrix Y with threshold b, shrinking singular values to promote low-rank matrix recovery.
(ii) AMCMDA_step1(interaction_matrix, disease_similarity, miRNA_similarity)
Constructs a heterogeneous graph matrix from disease similarity, interaction, and miRNA similarity matrices, and performs the first step of AMC to generate a refined association matrix.
Before running, the parameter 	r should be adjusted according to the optimal parameters of the called data set.
(iii) AMCMDA_step2(t, A, B)
Iteratively updates matrices to complete the association matrix via matrix decomposition and thresholding, based on inputs t, and singular vectors A and B.
Before running, the parameters α and β should be adjusted according to the optimal parameters of the called data set.

(3) Prediction and Similarity Calculation Functions
This module provides functions for predicting microRNA-disease associations and calculating similarity matrices based on interaction data.

(i) generate_prediction_score(interaction_matrix, disease_similarity, miRNA_similarity)
Generates the predicted association score matrix by performing matrix completion using AMC.
(ii) calculate_gaussian_similarity(interaction_matrix, num_diseases, num_miRNAs)
Computes Gaussian similarity matrices for diseases and miRNAs based on their interaction profiles.

(4) Run_Prediction_Model
Runs the disease-miRNA interaction prediction model and outputs the sorted prediction results to an Excel file.

(5) MiRNA-Disease Association Prediction Pipeline
Imports necessary system-related modules and runs the overall prediction model.


##  Data Description

The three dataset are derived from and includes:

[HMDD v1.0]
- 271 miRNAs
- 137 diseases
- 1395 validated associations

[HMDD v2.0]
- 495 miRNAs
- 383 diseases
- 5430 validated associations

[HMDD v3.2]
- 788 miRNAs
- 374 diseases
- 8968 validated associations

Integrated similarities:
- miRNAs: functional similarity (via MISIM method) and GIP
- Diseases: semantic similarity (MeSH DAG) and GIP

For details, refer to our manuscript's **section 2.1 – 2.2**.


## Citations

We acknowledge and thank the following foundational works:

- [HMDD v1.0](https://doi.org/10.1371/journal.pone.0003420)

- [HMDD v2.0](https://doi.org/10.1093/nar/gkt1023)

- [HMDD v3.2](https://doi.org/10.1093/nar/gky1010)


##  Contact

For any questions or suggestions:

> Email**: tangyong_301AT163.com (corresponding author)
