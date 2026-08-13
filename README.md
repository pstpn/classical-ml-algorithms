# Classical machine learning

Seven studies across the classical algorithms, plus a coursework that puts several of them
against each other on one dataset. Where an algorithm is simple enough to write out, it is
written out rather than imported, and the library version is kept alongside as the control.

| Study | Task |
|-------|------|
| [Clustering](1_clustering) | k-means++ and DBSCAN written from scratch on the composition of ancient ceramics |
| [Association rules](2_associative_rules) | Apriori written from scratch against FP-Growth on retail baskets |
| [SVM](3_svm) | Detecting the P300 response in EEG recordings |
| [Gradient boosting](4_gradient_boosting) | Recognising human activity from phone sensors |
| [Random forest](5_random_forest) | Multiclass classification with the tree depth tuned on a validation split |
| [Multilayer perceptron](6_mlp) | Telling edible mushrooms from poisonous ones |
| [Exploratory analysis](eda) | Entropy, information gain and split information computed by hand |
| [Coursework](course) | Four models compared on the Wine Quality dataset, with a written report |

Datasets are tracked with DVC where they are too large to commit.
