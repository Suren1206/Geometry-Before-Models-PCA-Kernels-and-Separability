# Lessons Learnt

(a) This project is focused on studying geometry-in-depth more than just finding a model which will provide best accuracy. So we embarked on a series of experiments to unearth geometric representation in various scenarios – which are listed  below

(b) The baseline model for geometric representation is Linear SVC but we consciously included Logistic regression. Linear SVC is margin based while Logistic Regression is likelihood based; The fact both performed similarly proves that the dataset is not sensitive to boundary philosophy.

(c) During PCA transformation, we had picked up 8 principle components which gave maximum accuracy compared to 4 pc and 12 pc. We had to pick up this one quite consciously since we found that  (a) the features are neither strongly collinear and that (b) among the 30 features, none can be clearly classified as redundant.

(d) In order to see the visual impact of PCA, we chose only the first 2 principal components deliberately which constituted only 62% of the overall variation. We compared the PCA plot against the picture of  manually chosen features which can explain 90% of deviation. Very clearly the latter showed more skewness compared to the PCA plot but when we tried SVC model upon both these variations, we could see the classification is far from accurate under both the models

(e) We also tried to swap the order of tasks – to perform PCA first before Train / Test split and compare the results against the standard process of splitting and then applying PCA. Since this dataset is quite a small one, there was no difference in accuracy metrics on account of data leakage.

(f) While trying out Non linear kernels, we tried to compare the models with optimized principle components as well models without PCA. It was interesting to note that Linear SVC with PCA components provided an accuracy of   0.9825  & only 1 False Negative while RBF SVC without PCA matched this performance at 0.9737 accuracy with Nil False Negative. However RBF SVC needed approximately 3 times the number of support vectros that Linear SVC needed.

(g) We introduced both the Polynomial and RBF kernel to study the geometic behaviour – former to test global nonlinear interactions and latter to test the local similarity structure. We found that Polynomial under-performed while RBF kernel without PCs brought results close to Linear SVC with PC  explaining that the underlying geometry is already close to linearly seprable once reasonably conditioned. 

(h) Between the two non linear kernel, the impact of PCAs was another interesting observation. We found that neither of them drastically improved the results after the PCA transformation. We neither discovered any interaction-driven structure (if Polynomial had drastically improved) nor discovered cluster-driven non linearity (in case of substantial improvement in RBF)

(i) When we tried the perturbed data set to have only 15% of Malignant records (against original 37 %), we found that the imbalance made the problem appear easier without fundamentally increasing geometric structure. Kernel methods did not uncover hidden nonlinear separability; instead, boundary complexity decreased as class tension reduced. (More details on perturbed data set experiment covered in Appendix)
