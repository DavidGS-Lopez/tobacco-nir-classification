# Geographical Origin Identification of Tobacco Leaves using NIR Spectroscopy
 

This project aims to create a multi-class classification model that is able to predict the geographical origin of a tobacco leaf from their near-infrared (NIR) spectra. The overall strategy consisted of three main steps: 

1. Exploratory data analysis (EDA) to get summary statistics to understand structure and remove possible outliers. Principal component analysis (PCA) was then conducted to visualize the data. 

2. Several preprocessing methods were applied to improve the quality of the raw data. After inspecting the PC-plots, the combination of *Savitzky–Golay 2nd derivative (SG2), Standard Normal Variate (SNV) and mean centering (MC)* showed the clearest cluster-separation and was chosen for further modeling. 

3. Several classification models were trained and optimized, and their performance was evaluated using macro F1-score and a separate test set. 


## Background
 
NIR spectra are sensitive to the chemical composition of organic matter. The composition of tobacco leaves is in turn influenced by soil chemistry and climate, which means that leaves from different countries may have subtly different spectral signatures. This project investigates how well those signatures can be used to identify where a sample was grown.

## Dataset
 
The data comes from Chen et al. (2026), who collected 347 tobacco leaf samples from six countries.

The dataset used in this project is included in the repository: [tobacco-nir-all.csv](/project/tobacco-nir-all.csv).
 
The original data is available from Mendeley Data: [DOI: 10.17632/9z7dgdtggk.1](https://data.mendeley.com/datasets/9z7dgdtggk/1) and is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


## Repository structure
 
This project consists of four Jupyter notebooks:
 
1. [eda](/project/eda.ipynb) which includes all the work related to the exploratory data analysis.
2. [preprocessing](/project/preprocessing.ipynb) which includes all the preprocessing methods applied on the data.
3. [models_SG2_data](/project/models_SG2_data.ipynb) which includes model development and results based on the SG2 + SNV + mc processed data.
4. [models_raw_data](/project/models_raw_data.ipynb) which includes model development and results based on the raw + mc data.

The project was carried out in Python using NumPy, pandas, Matplotlib Pyplot, SciPy, scikit-learn, and XGBoost. A [requirements.txt](/project/requirements.txt) file with the package versions used in this project is provided to facilitate reproducibility.

## Results (short summary)
Using the Savitzky-Golay 2nd derivative + SNV + mean-centred spectra, all five models achieved relatively high test performance. The learning curves and gap analysis show that preprocessing substantially stabilises the flexible models and that Partial Least Squares Discriminant Analysis (PLS-DA) and Support Vector Machine (SVM) are the most robust choices for the dataset.

The preprocessing is clearly beneficial for most models, but Partial Least Squares Discriminant Analysis (PLS-DA) modeled on raw + MC  performed the best with 0.969 macro F1-score.

##### Test and cross-validation performance for the best model-preprocessing combinations:

| Model + preprocessing    | Accuracy | Macro F1 | Weighted F1 | CV macro F1 |
|--------------------------|----------|----------|-------------|-------------|
| SVM (SG2 + SNV + MC)     | 0.943    | 0.926    | 0.942       | 0.925       |
| PLS-DA (raw + MC)        | 0.971    | 0.969    | 0.971       | 0.968       |


## References

Hexin Chen, Junwei Guo, Beibei Li, et al. “A dataset for geographical origin identification of tobacco
leaves from multiple countries using near-infrared spectroscopy and chemometric analysis”. In:
Data in Brief 64 (2026), p. 112418. DOI: 10.1016/j.dib.2025.112418.
