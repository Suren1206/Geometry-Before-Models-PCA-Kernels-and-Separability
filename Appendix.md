# Appendix — Geometry Under Class Prior Distortion

The original dataset consisted of 569 records, out of which 212 were malignant (approximately 37%). To study how geometric representation behaves under imbalance, we reduced the malignant cases to 63, bringing the proportion down to roughly 15%, while retaining all benign cases. No labels were modified; only records were removed.
Observations

First, both Logistic Regression and Linear SVC achieved training accuracy of 1 and test accuracy of 98.8%, compared to earlier results of approximately 98.7% (train) and 96.5% (test). The number of false negatives reduced from 4 to 1. This apparent improvement must be interpreted cautiously. Since the proportion of malignant cases decreased, the evaluation metric became less sensitive to errors in the minority class. The geometry did not necessarily improve; the class prior changed.

Second, the PCA variance spectrum remained broadly similar. However, optimal classification performance was now achieved with 6 principal components instead of 8. This suggests that while PCA itself is label-agnostic, removing malignant samples slightly altered the empirical covariance structure. The contribution of malignant cases to overall variance weakened, allowing fewer components to support comparable classification performance.

Third, with the optimized principal components, all three SVC variants—Linear, Polynomial, and RBF—produced nearly identical prediction results. The earlier false positive was eliminated, but one false negative remained. This indicates that nonlinear capacity did not reveal additional separability under imbalance.

Fourth, without PCA transformation, RBF SVC and Linear SVC achieved similar accuracy (~0.98), while Polynomial SVC performed slightly lower (~0.97). Again, nonlinear kernels did not provide a meaningful advantage over linear separation.

Fifth, support vector counts changed significantly. For Linear and RBF kernels, support vector usage increased to nearly half of the dataset. For the Polynomial kernel, support vectors dropped sharply from approximately 29% to 8%. This reflects reduced boundary tension: with fewer malignant cases constraining the margin, complex boundaries became less necessary.
Interpretation

### (a) Reducing the proportion of malignant cases made the classification task appear easier, even though the overall variance structure of the dataset remained broadly similar. The PCA spectrum remained broadly similar because PCA depends only on feature covariance. However, removing malignant samples slightly reduced their contribution to the overall variance structure, which explains why fewer principal components were sufficient for optimal classification. However, classification performance improved largely due to reduced minority pressure on the decision boundary.

### (b) The imbalance made the problem appear easier without fundamentally increasing geometric structure. Kernel methods did not uncover hidden nonlinear separability; instead, boundary complexity decreased as class tension reduced.

### (c) This controlled perturbation reinforces an important insight: apparent improvements in accuracy under imbalance must be interpreted in light of class distribution and margin dynamics, not assumed to reflect improved representational quality.
