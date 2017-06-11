### This pages for students who takes Pattern Recognition Lab (CSI 416).

### Syllabus :


## Key notes :
  1. Features / Attributres
  2. Feature-values & Attributre-values
  3. Class & Class-Attributes
  4. Instances / Records / Vectors / Tuples
  5. Two-class dataset & Multi-class dataset ( When number of class-values is gretter than 2. )
  6. High-dimensional ( When number of feature is gretter than 10. )
  7. Balanced dataset vs Imbalanced dataset
  8. What is overfitting of a dataset ?
  9. Supervised learning vs. Unsupervised learning
  10. Classification, Regression, Clustering


### Classification
- Rule Classifiers
  - ZeroR Classifier
  - OneR Classifier
  
- KNN Classifier
- SVM Classifier
- Naive Bayes Classifier
- Decision Tree Classifier
  - Gini
  - ID3
  - C4.5/C5.0 (J48)
  

### Clustering
- KMeans
- Hierarchical


```sh
cd /home/..
ls
mkdir MRZ
```

```py
"""
=============================================
Multiclass classification with under-sampling
=============================================

Some balancing methods allow for balancing dataset with multiples classes.
We provide an example to illustrate the use of those methods which do
not differ from the binary case.

"""

# Authors: Guillaume Lemaitre <g.lemaitre58@gmail.com>
# License: MIT

from sklearn.datasets import load_iris
from sklearn.svm import LinearSVC
from sklearn.model_selection import train_test_split

from imblearn.under_sampling import NearMiss
from imblearn.pipeline import make_pipeline
from imblearn.metrics import classification_report_imbalanced

print(__doc__)

RANDOM_STATE = 42

# Create a folder to fetch the dataset
iris = load_iris()
# Make the dataset imbalanced
# Select only half of the first class
iris.data = iris.data[25:-1, :]
iris.target = iris.target[25:-1]

X_train, X_test, y_train, y_test = train_test_split(iris.data, iris.target,
                                                    random_state=RANDOM_STATE)

# Create a pipeline
pipeline = make_pipeline(NearMiss(version=2, random_state=RANDOM_STATE),
                         LinearSVC(random_state=RANDOM_STATE))
pipeline.fit(X_train, y_train)

# Classify and report the results
print(classification_report_imbalanced(y_test, pipeline.predict(X_test)))
```
