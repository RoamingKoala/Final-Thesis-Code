# Pedestrian Movement Clustering in High-Density Scenarios

This repository contains data processing, threshold detection, and clustering analysis tools for studying pedestrian movement patterns in high-density rushing scenarios across multiple experiments. It includes scripts for data cleaning, segmentation, and clustering using DBSCAN and hierarchical methods.

## Data Preprocessing

1. **Initial Data Cleaning (`initial_processing1.ipynb`, `initial_processing2.ipynb`, `initial_processing3.ipynb`)**  
   For each of the three experiments, data is cleaned by renaming columns and removing the first five rows of transferred data. The cleaned data for each experiment is saved as `ExperimentX_abnormalvalue.xlsx`, where `X` refers to the specific experiment number (1, 2, or 3). This cleaned data is then used for subsequent statistical analysis.  
   
   **Output:**  
   - `Experiment1_abnormalvalue.xlsx`  
   - `Experiment2_abnormalvalue.xlsx`  
   - `Experiment3_abnormalvalue.xlsx`

2. **Statistical Analysis**  
   For each experiment, the cleaned data is analyzed to determine the top and bottom 2.5% extreme values for distance and speed. These thresholds are crucial for the next step of data preprocessing.

3. **Further Data Processing (`CleanData1.ipynb`, `CleanData2.ipynb`, `CleanData3.ipynb`)**  
   Using the previously identified threshold values, the data for each experiment is further filtered to extract complete pedestrian trajectories. The resulting data for each experiment is saved as an Excel file, and trajectory plots are generated. These files and images are stored in the following paths:

   **Output:**  
   - Processed data:  
     - `1.8/ResultWholeDistance/Experiment1_Data.xlsx`  
     - `1.8/ResultWholeDistance/Experiment2_Data.xlsx`  
     - `1.8/ResultWholeDistance/Experiment3_Data.xlsx`  
   - Trajectory plots:  
     - `1.8/Experiment1_AllTrajectories`  
     - `1.8/Experiment2_AllTrajectories`  
     - `1.8/Experiment3_AllTrajectories`

## Threshold Detection and Validation

4. **Threshold Detection (`FindThreshold.ipynb`)**  
   A Kernel Density Estimation (KDE) method is used to identify the distance threshold for "high-density rushing scenarios." The determined threshold is `1.86`.

5. **Threshold Validation**  
   The threshold value of `1.86` is validated through two separate processes:
   - **`Density volume.ipynb`**: Generates a density map to visualize the density distribution.
   - **`1.86 threshold statistical verification.ipynb`**: Conducts statistical analysis on the data, split by the `1.86` threshold, revealing significant differences between the two groups.

## Trajectory Segmentation

6. **Trajectory Segmentation (`CleanData1_only1.86.ipynb`, `CleanData2_only1.86.ipynb`, `CleanData3_only1.86.ipynb`)**  
   After validating the `1.86` threshold, the complete pedestrian trajectories for all three experiments are segmented, retaining only the portions where the distance is less than `1.86`. The segmented data is saved in new files for each experiment.

   **Output:**  
   - Segmented data:  
     - `1.8/1.86/Experiment1.xlsx`  
     - `1.8/1.86/Experiment2.xlsx`  
     - `1.8/1.86/Experiment3.xlsx`

## Clustering Analysis

7. **Data Extraction for Clustering**  
   Data necessary for clustering analysis is extracted from the processed datasets, and two combined files are generated:
   - **`Cluster_Data_Wholedistance_withposition(cleaned).ipynb`**: This script extracts the full distance trajectory data for all three experiments.
   - **`Cluster_Data_1.86_withposition(cleaned).ipynb`**: This script extracts the data where the distance is less than `1.86` for all three experiments.

   **Output:**  
   - Extracted data for clustering:  
     - `Cluster_Data_Wholedistance_withposition(cleaned).xlsx`  
     - `Cluster_Data_1.86_withposition(cleaned).xlsx`

8. **Clustering Methods**  
   The clustering analysis is performed on the extracted data using two methods:
   - **DBSCAN Clustering (`DTW_DBSCAN_Cluster1.86.ipynb`)**: Performs DBSCAN clustering based on Dynamic Time Warping (DTW).
   - **Hierarchical Clustering (`DTW_Hierarchical_Cluster1.86.ipynb`)**: Performs hierarchical clustering using DTW.  
   
   Clustering results are saved in the following path:

   **Output:**  
   - Clustering results:  
     - `1.8/ClusterResult/cluster_result_dbscan.csv`
     - `1.8/ClusterResult/cluster_result_hierarchy.csv`
## Pattern Recognition

9. **Pattern Recognition from Clustering Results**  
   After the clustering analysis, the following notebooks are used to identify distinct behavioral patterns in the clustered data:
   - **`DTW_DBSCAN_Pattern_Recognition.ipynb`**  
   - **`DTW_Hierarchical_Pattern_Recognition.ipynb`**

   These scripts analyze the patterns identified from the DBSCAN and hierarchical clustering results.

---

## File Structure

```plaintext
.
├── initial_processing1.ipynb          # Data cleaning for Experiment 1 (renaming, removing rows)
├── initial_processing2.ipynb          # Data cleaning for Experiment 2
├── initial_processing3.ipynb          # Data cleaning for Experiment 3
├── CleanDataX_only1.86.ipynb          # Trajectory segmentation (distance < 1.86)
├── Cluster_Data_Wholedistance_withposition(cleaned).ipynb # Data extraction for clustering (full trajectory)
├── Cluster_Data_1.86_withposition(cleaned).ipynb          # Data extraction for clustering (distance < 1.86)
├── DTW_DBSCAN_Cluster1.86.ipynb       # DBSCAN clustering analysis
├── DTW_Hierarchical_Cluster1.86.ipynb # Hierarchical clustering analysis
├── results/                           # Directory for storing clustering results
│   ├── cluster_result_dbscan.csv      # DBSCAN clustering results
│   └── cluster_result_hierarchy.csv   # Hierarchical clustering results
├── data/                              # Directory for raw and processed data
│   ├── Experiment1_abnormalvalue.xlsx # Cleaned data for Experiment 1
│   ├── Experiment2_abnormalvalue.xlsx # Cleaned data for Experiment 2
│   ├── Experiment3_abnormalvalue.xlsx # Cleaned data for Experiment 3
│   ├── Experiment1_Data.xlsx          # Processed data for Experiment 1 (full trajectory)
│   ├── Experiment2_Data.xlsx          # Processed data for Experiment 2
│   └── Experiment3_Data.xlsx          # Processed data for Experiment 3
├── Cluster_Data_Wholedistance_withposition(cleaned).xlsx  # Dataset for clustering (full trajectory)
├── Cluster_Data_1.86_withposition(cleaned).xlsx           # Dataset for clustering (distance < 1.86)
└── README.md                          # Project documentation


