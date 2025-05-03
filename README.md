# Bitcoin-Ransomware-Classification
## Introduction
This project aims to identify ransomware-related Bitcoin addresses by analyzing transaction patterns of several features. The Bitcoin Heist Ransomware Address dataset:https://archive.ics.uci.edu/dataset/526/bitcoinheistransomwareaddressdataset, covering over 2.9 million transactions from 2009 to 2018, was used to extract relevant patterns.

To tackle the challenge of identifying ransomware- related Bitcoin addresses, we first preprocess the dataset to extract relevant features and clean the data, then we experiment with oversampling minority classes and utilizing four different classification algorithms to evaluate their effectiveness in identifying malicious addresses. The algorithms tested include two decision- tree-based methods: Random Forest and LightGBM, along with SVM and DNNs.

## Preprocessing: 

1-Feature Engineering: /n
-Created two new features:
-Merge Intensity = weight × count
-Loop Complexity = looped × length
-Removed the address ID feature as it was not informative for pattern learning.

2-Class Imbalance Handling:
-The dataset was heavily imbalanced, dominated by the white class (over 2.8 million samples).
The white class (non-ransomware addresses) was excluded since it irrelevant for classifying different types of ransomeware .
-Classes with fewer than 100 samples were also removed.
-Result: 8 ransomware-related classes remained with a total of 41,060 samples.

3-Feature Scaling and Encoding:
Applied z-score standardization to all features (zero mean, unit variance).
Used label encoding to convert categorical class labels into integer values.

4-Data Splitting:
Performed stratified sampling to maintain class distribution:
80% of data for training, 20% for testing.
The training set was further split: 80% training, 20% validation for hyperparameter tuning.

## Classification algorithims performance analysis: 

Different hyperprameter tuning was performed on each of the models; LightGBM emerged to be the top performer In the implementation it was subjected to the optimization of hyperparameters including the number of estimators, learning rate, number of leaves, subsampling rate , and column sampling rate; this was done by 10 randomized iterations and 3-fold cross-validation. The best configuration identified by the random search included the following hyperparameters: number of estimators set to 500,learning rate set to 0.2,number of leaves set to 100, subsampling rate set to 0.8, and column sampling rate set to 0.8.
The model demonstrated near-perfect performance of 97.17% accuracy on the validation set.
 
Overall, LightGBM and Random Forest with a slightly less performance proved to be the most effective algorithms for this classification task, showing high accuracy and balanced performance across all metrics. The SVM and DNN models, while still performing reasonably well, were outperformed by these tree-based methods.

