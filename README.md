**Author:** Jessica Janko
**Date Created:** 10-06-2026
**Last Modified:** 10-19-2026

# GLENDA Endometriosis Dataset: Exploratory Data Analysis

## Overview
This project focuses on **Exploratory Data Analysis (EDA)** of the **GLENDA (Gynecologic Laparoscopy ENdometriosis DAtaset).**
The goal is to explore the dataset's composition, image and annotation characteristics, and data quality through statistical analysis and visualization, identifying patterns relevant to future research on endometriosis recognition in laparoscopic imaging.

## Dataset
**GLENDA** (Gynecologic Laparoscopy ENdometriosis DAtaset) is a medical imaging dataset containing 25,682 images collected during more than 400 gynecologic laparoscopy surgeries. The dataset was created to support the development of automated approaches to endometriosis recognition.

The dataset contains two image groups: `no_pathology` (images without endometriosis) and `pathology` (images containing endometriosis). Annotations are available for a subset of the data and include four lesion categories: `peritoneum`, `ovary`, `uterus`, and `die`.

| Dataset Component     | Count |
| :-------------------- | :---- |  
| Total Images          | 25682 |
| `no_pathology` Images | 13438 |
| `pathology` Images    | 12244 |
| Annotation Files      | 520   |
| Annotated Images      | 302   |
| Unannotated Images    | 11942 |

## Data Cleaning

Exact duplicate images were identified using SHA-256 hashing. Duplicate entries were removed from copied image path lists 
for both groups, keeping only one entry for each set of identical images. The original image files were not deleted but were
excluded from further analysis.

| Dataset Component | Original Count | Images Removed | % Removed | Count After Cleaning |
| :---------------- | :------------- | :------------- | :-------- | :------------------- |
| no_pathology      | 13438          | 324            | 2.411     | 13114                |
| pathology         | 12244          | 171            | 1.397     | 12073                |
| Total             | 25682          | 495            | 1.927     | 25187                |

Two zero-size annotations were identified during annotation integrity checks and removed from the cleaned dataset.

| Dataset Component | Original Count | Annotations Removed | % Removed | Count After Cleaning |
| :---------------- | :------------- | :------------------ | :-------- | :------------------- | 
| Annotation Files  | 520            | 2                   | 0.385     | 518                  |

## Exploratory Data Analysis: Methodology
1. Dataset Overview and Integrity
- Summarized counts across `pathology` and `no_pathology` groups, along with annotation counts across the four lesion categories.
- Examined image and annotation frequency distributions by lesion category.
- Analyzed the frequency distribution of annotation density per image.
- Conducted data integrity checks to identify duplicate images and empty annotation files, as well as verified file accessibility and consistency.
- Performed data cleaning procedures to address identified issues. 
   
2. Lesion Annotation Characteristics
- Calculated summary statistics for annotation areas, including the average, median, standard deviation, minimum, and maximum of each lesion category.
- Examined annotation area distributions overall and by lesion type.
- Identified annotation area outliers and analyzed their proportions by lesion type, with a focus on peritoneum annotations.
- Investigated the spatial distributions of lesions using annotation centroids and a heatmap. 
   
3. Image Quality and Color Metrics
- Performed brightness, contrast, and sharpness analysis to compare their distributions between image groups.
- Analyzed RGB color channel distributions.
   
4. Dataset Visual Exploration and Annotation Visualization
- Visually explored sample images across image groups and documented observable characteristics and differences. 
- Visualized annotation overlays to assess their spatial alignment with images and examine the relationship between annotation regions and visible lesion features.
- Examined multi-label instances through image and annotation overlays, documenting notable characteristics. 
   
5. Visual Image Quality Assessment
- Inspected images with extreme brightness, contrast, and sharpness metric values from Section 3 to assess potential image quality concerns.
- Documented observed quality concerns, unusual visual characteristics, and considerations for future analysis.
   
6. Image Similarity and Redundancy Analysis
- Visually inspected consecutive frames to address potential redundancy between sequential images.
- Compared SSIM values for sequential and randomized frame pairs to assess the degree of structural similarity between consecutive frames relative to randomly paired images.
   
## Key Findings   
Dataset Composition
   - Peritoneum is the most represented lesion class in the dataset.
   - Video sequences are not fully independent, as exact duplicate frames were found across parent video sequences.

Annotation Characteristics
   - Annotation sizes meaningfully vary across lesion classes.
   - Some annotated regions were visually subtle or ambiguous, illustrating the challenges of interpreting laparoscopic images and recognizing endometriosis.

Image Quality
   - Brightness, contrast, and sharpness distributions showed substantial overlap between the `pathology` and `no_pathology` image groups.
   - Some frames contain obstructions and visual disruptions, including surgical instruments, glare, and lighting issues that raise image quality concerns.
     
Image Similarity
   - Sequential frames have substantially higher structural similarity than randomized image pairs.

## Usage Instructions
The GLENDA dataset is not included in this repository and must be downloaded separately to run the notebook.
The HTML export is provided for convenient, read-only access to the analysis. 

### Viewing the HTML Export
Open the `glenda-eda.html` in a web browser to explore the analysis, visualizations, and results without installing Python, Jupyter Notebook, or downloading the GLENDA dataset.

### Running the Jupyter Notebook
To run the notebook locally, follow these steps:
1. **Download the dataset.** Obtain GLENDA v1.0 from the [official dataset page](https://ftp.itec.aau.at/datasets/GLENDA/v1_0/).
2. **Extract the dataset.** Unzip the downloaded folder and ensure the GLENDA_v1.0 folder is available locally.
3. **Set up the project directory.** Place the `GLENDA_v1.0` folder in the same directory as glenda-eda.ipynb.
4. **Install the required dependencies.** Install the Python packages listed in requirements.txt in your Python environment. 
5. **Open the notebook.** Open glenda-eda.ipynb using JupyterLab or Jupyter Notebook. These environments can be installed and launched independently or accessed through distributions such as Anaconda.
6. **Run the notebook.** Execute the cells in order, starting from the beginning. Ensure the dataset paths are correct before running the EDA notebook. 
   
## Requirements 
- Python
- JupyterLab or Jupyter Notebook 
- The GLENDA v1.0 dataset (must be downloaded separately).

### Python Packages
- NumPy
- pandas
- Pillow
- Matplotlib
- SciPy
- scikit-image

Install the required Python packages by running `pip install -r requirements.txt`.

## Dataset License and Citation
GLENDA is licensed under Creative Commons Attribution-NonCommercial 4.0
International (CC BY-NC 4.0, https://creativecommons.org/licenses/by-nc/4.0/).

A. Leibetseder, S. Kletz, K. Schoeffmann, S. Keckstein and J. Keckstein. 2020.
GLENDA: Gynecologic Laparoscopy Endometriosis Dataset. To appear: In Proceedings of the
26th International Conference on Multimedia Modeling, MMM 2020. Springer, Cham.
