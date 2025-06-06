# ALS NIV Prediction using Temporal Pattern Mining

## Overview

This project aims to predict the need for Non-Invasive Ventilation (NIV) in Amyotrophic Lateral Sclerosis (ALS) patients using temporal pattern mining and machine learning techniques. The project utilizes a combination of static patient features and temporal data from disease follow-up to learn disease progression patterns and build a predictive model.

This project is based on a reduced part of the work published by Martins et al. (https://ieeexplore.ieee.org/document/9426397).

## Project Structure

```
Dataset_NIV_Evolution_180.csv     # NIV evolution data (class labels)
Dataset_Static_Features.csv        # Static patient features
Dataset_Temporal_Features.csv      # Temporal patient features
PD_202425_Project2.ipynb            # Jupyter notebook with project code and analysis
spmf.jar                            # Sequential Pattern Mining Framework (SPMF)
```

## Dependencies

-   Python 3.x
-   Jupyter Notebook
-   Pandas
-   Scikit-learn
-   Matplotlib
-   Seaborn
-   SPMF (Sequential Pattern Mining Framework)

## Setup

1.  **Install Python Dependencies:**

    ```bash
    pip install pandas scikit-learn matplotlib seaborn
    ```

2.  **Download SPMF:**

    *   Ensure that `spmf.jar` is in the project directory. If not, download it from [SPMF website](http://www.philippe-fournier-viger.com/spmf/).

## Usage

1.  **Data Preprocessing:**

    *   Load the datasets (`Dataset_Static_Features.csv`, `Dataset_Temporal_Features.csv`, `Dataset_NIV_Evolution_180.csv`) using Pandas.
    *   Preprocess the temporal data to remove missing values and filter patients based on the number of time-points (minimum 2, maximum 5).
    *   Aggregate temporal features into intervals as defined in the notebook.

2.  **Sequence Database Creation:**

    *   Transform the preprocessed temporal data into a sequence database format suitable for SPMF.
    *   The notebook contains the function `create_sequence_db_df` to perform this transformation.

3.  **Sequential Pattern Mining:**

    *   Use the `Fournier08` algorithm from SPMF to compute closed sequential patterns.
    *   Run the SPMF command via `os.system` in the notebook. Example:

        ```bash
        java -jar spmf.jar run Fournier08-Closed+time sequences.txt output.txt 25% 0 5 0 5
        ```

    *   Filter trivial patterns of length 1.

4.  **Model Training and Evaluation:**

    *   Create a training set by combining static features and sequential patterns.
    *   Train a Random Forest classifier using 5-fold stratified cross-validation.
    *   Evaluate the model's performance using accuracy, ROC AUC, and classification reports.

## Key Findings

*   **Temporal Patterns:**
    *   The most frequent patterns involve transitions from preserved to declining function.
    *   3-timepoint patterns provide an optimal balance between temporal richness and pattern frequency.
*   **Feature Importance:**
    *   Sequential patterns account for a significant portion of the predictive power.
    *   ALSFRS-R and respiratory function (R) scores are consistently important features.
*   **Model Performance:**
    *   Achieved a cross-validation accuracy of approximately 55-57%.
    *   The 20% minimum support configuration shows improved stability with lower standard deviation.
*   **Patient Clustering:**
    *   Patient clustering based on sequential patterns reveals subgroups with different NIV rates.

## Recommendations

*   Consider ensemble methods combining temporal and static features.
*   Investigate feature engineering techniques for temporal sequences.
*   Validate findings on external datasets.
*   Explore additional temporal features or longer observation windows.

## Team

*   Daniel Carvalho - 64350
*   Gabriel Meirinho - 64873
*   Rita Silva - 56798