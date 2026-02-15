#(A) About Dataset
We intend to study the various ways in which data can be represented and see their impact on separability / classification
UCI Breast Cancer (Wisconsin) was chosen which has ~30 numerical features (perfect PCA territory) & well known for studying margin, support vectors, and overconfidence.This dataset further serves the twin objectives of this project:
(1) Clear distinction between representation failure & classification failure
(2) Representation of geometry of a diagnostic decision by being class-balanced

Phase 1:  Performance of Basic Models
After basic sanity checks and review of the data pattern, we trained a logistic regression model and a linear SVC with an 80:20 train–test split. Both of them yielded a training accuracy of 0.9868 and test accuracy of 0.9649, indicating strong performance under the linear class of models. We also found that there were issues with separability — specifically with overlap of the negative class (Benign) into the positive class (Malignant), resulting in false negatives.

In terms of numbers, when we looked at accuracy metrics, we found that out of the test sample (which works out to 114, being 20% of the total count – 570 records), there were four cases of false negatives

Phase 2 — PCA as a Conditioning Tool
We introduced PCA to examine whether variance-based dimensionality reduction improves separability.

Although approximately 8 principal components were required to explain around 90% of total variance, classification improvement was not driven by variance coverage alone. Linear SVC showed improved performance with PCA, while nonlinear kernels did not consistently benefit.

This indicates that PCA conditioned the feature space in a way that supported linear separation but did not fundamentally alter class geometry. PCA reduced dimensional redundancy without unlocking hidden nonlinear structure.

Phase 3 — PCA Misused (Deliberately)
Since one of the primary goals of this project is to study geometric behavior, we explored dimensionality reduction (PCA) beyond restricting ourselves to an optimized choice of principal components.

Using very few principal components (e.g., 2 PCs explaining ~62% variance) resulted in clear degradation of classification performance. Selecting components manually based on feature intuition also underperformed relative to systematic PCA selection.

Applying PCA before train–test split did not materially change performance in this dataset, suggesting limited sensitivity to that specific misuse under current conditions.

These experiments confirmed that PCA must be used as a geometric conditioning tool, not as a blind variance maximization strategy. Dimensionality reduction alone does not guarantee improved separability.

Phase 4 — Kernels vs Linear Boundary
In this phase, we compared Linear SVC, Polynomial SVC, and RBF SVC, both with and without PCA transformation.
Linear SVC performed best when combined with 8 principal components. RBF SVC performed slightly better in the original feature space than with PCA. Polynomial SVC consistently underperformed relative to the other two variants and showed minimal sensitivity to PCA transformation.

The performance differences between the best Linear and best RBF configurations were marginal. This indicates that the dataset does not exhibit strong nonlinear structure requiring kernel expansion.

Support vector analysis provided additional insight. RBF required substantially more support vectors than Linear SVC, indicating a more complex boundary. However, this added complexity did not translate into proportionate performance gains.
Overall, nonlinear kernels increased flexibility but did not uncover hidden separability beyond what linear models already captured after reasonable conditioning.
Phase 5 — Representation–Boundary Interaction
This phase examined how dimensionality reduction and kernel expansion interact when applied together.
The experiments revealed that PCA primarily benefits linear separation by conditioning the feature space, while nonlinear kernels derive limited additional advantage from PCA transformation. In particular, the combination of PCA and RBF did not materially outperform simpler configurations.
The key insight is that increased representational flexibility did not uncover new separability. Instead, it redistributed complexity across transformation and boundary choice. When PCA simplified geometry, linear models benefited. When raw feature space was preserved, RBF absorbed local variation. However, the empirical gains remained marginal.
This phase clarified that combining PCA and kernels does not automatically manufacture superior structure. The interaction must be evaluated in terms of both performance gain and boundary complexity.
Phase 6 — Consolidated Insights
PCA is justified when dimensionality reduction improves conditioning without degrading class structure, not merely because it explains a high percentage of variance. In this case, though we needed 8 principle components to explain 90% of variations it was helpful only because  PCA conditioned the space to support a linear separation which we found in the improvement of Linear SVC.
If linear models remain insufficient after reasonable conditioning, nonlinear kernels may be explored. It is always better to verify direct non linear transformation and compare the results with PCA-transformed data because there is a possibility PCA might have deteriorated either in local or global or in both feature space
If PCA does not materially degrade classification performance, it may safely be combined with nonlinear models. But we should be guarded to reach that stage after trying the base models and transformations one step at a time.
Also we should bear in mind that we should look at the cost of separability in terms of support vectors used and their percentage of the data set & also the train-test robustness before making any conclusion about the model accuracy since geometry depends on these factors.
Robust classification is more a consequence of Geometrically suitable modeling 
