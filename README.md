# Prediction of protein isoform by semi supervised learning
This project was done for the course 02456 Deep Learning at DTU in the fall of 2022. The goal was to investigate the prediction performance of using semi-supervised learning in the form of a Variational AutoEncoder (VAE) followed by a standard feed-forward neural network for the prediction of protein isoform expressions from gene expression data.
This repository contains data subsets, model scripts, model trained on the subsets, project poster and the project report.


## Scripts
The jupyter notebooks in the base directory replicates all major findings of the project. There are two version of each script except for the data loading and transformation script: One version contains the settings and results used for the full data, and the other version (prefixed by TESTING) can be used with the small data subsets provided here for purely illustrative purposes.

### 1_Load_and_transform
This notebook loads the raw datasets, provides some basic visualizations of data distributions and then performs transformations of the data so that it can used for our learning scripts. Only a single file is provided as the full datasets are not made available here. However, in the 'Define file paths' section a swith to use the full datasets can be made. These datasets are available on the DTU HPC at /dtu-compute/datasets/iso_02456.

### 2_Variational_Autoencoder_Gridsearch
This script is used to search the hyperparameter space of our Variational Autoencoder using a simple grid search approach. Due to long runtimes and limited computational resources the space searched was nowhere near exhaustive.

### 3_Variational_Autoencoder
This is the main script for training the VAE model on the large ARCHS4 gene expression dataset to learn a suitable latent space. 

### 4_Encode
This script takes a trained model .pth file and encodes the smaller GTEX gene expression dataset into the latent space.

### 5_Lasso_regression_baseline
Baseline lasso regression to evaluate the performance of our approach against.

### 6_Regression_model
This notebook takes the GTEX gene expression data which has been encoded into the latent space and uses it for protein isoform predictions. In the TESTING version, density calculation for the output plot has been disabled as it slows down the script noticably. 

## Data
The /Data/iso_02456/ directory contains subsets of all the datasets provided for the project:
- archs4_gene_expression_subset.tsv: Subset of the large gene expression dataset used to train the VAE model
- gtex_annot.tsv: Tissue annotations for the samples of the GTEX datasets
- gtex_gene_expression_subset.tsv: Subset of the smaller GTEX gene expression dataset. These are the predictor variables for the regression model.
- gtex_gene_expression_subset_transposed.tsv: As above, transposed version.
- gtex_isoform_expression_subset.tsv: Subset of the GTEX protein isoform expression dataset. These are the target variables for the regression model.
- gtex_isoform_expression_subset_transposed.tsv: As above, transposed version.

The /Data/ directory contains various transformed versions of the datasets:
- archs4_data_transformed.npy: The ARCHS4 gene expression data subset after log2-transformation with a pseudocount of one and quantile tranformation.
- gtex_gene_expression.npy: The GTEX gene expression data subset after log2-transformation with a pseudocount of one and quantile tranformation.
- gtex_gene_expression_encoded.npy: The GTEX gene expression data subset encoded by the VAE model into the latent space.
- gtex_gene_pca_4.npy: The first 4 principal components of the GTEX gene expression data subset. Used in evaluation of the VAE.
- gtex_isoform_expression.pickle: Pickled version of GTEX isoform expression data subset after log2-transformation with a pseudocount of one.
- gtex_isoform_expression_965_subset.npy: Numpy file with the 965 isoforms we have done our analysis on.
- gtex_isoform_expression_965_subset.pickle: Pickled file with the 965 isoforms we have done our analysis on.

## Model
This directory contains a single VAE model trained on the the small subset of the ARCHS4 dataset provided here.

