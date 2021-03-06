# Anomaly Detection
_Anomaly detection_ refers to the problem of finding patterns in data that do not conform the expected behavior.
These nonconforming patterns are often referred to as anomalies or outliers. Anomaly detection finds extensive use in a wide variety of applications such as fraud detection for credit cards, insurance or health care, intrusion detection in cyber-security, fault detection in safety critical systems, and military surveillance for enemy activities.
## What are Anomalies
Anomalies are patters in data that do not conform to a well defined notion of normal behavior.
## Related Topics
[Noise Accomodation](Noise Accomodation.md)
[Novelty Detection](Novelty Detection.md)

Solutions for these three topics are generally interchangeable.

## Challenges

At an abstract level, anomaly is defined as a pattern that does not conform to expected normal behavior.
Therefore, a straightforward approach is to define
* Defining a normal region that encompasses every possible normal behavior is very difficult. In addition, the boundary between normal and anomalous behavior is often not precise. Thus an anomalous observation that lies near the border might be normal and vice versa.
* When anomalies are the result of malicious actions, the malicious adversaries often adapt themselves to make the anomalous observations appear normal, thereby making the task of defining normal behavior more difficult.
* In many domains normal behavior is evolving
* The exact notion of anomaly is different across domains.
* Availability of labeled data for training/validation of models used by anomaly detections techniques is usually a major issue.
* Often data contains noise similar to the actual anomalies.

## Types of Anomaly
Anomalies can be classified into following three categories:

### Point Anomalies
If an individual data instance can be considered as anomalous with respect to the rest of the data, then the instance is termed a point anomaly. This is the simplest type of anomaly.

### Contextual Anomalies
If  a data instance is anomalous in a specific context, but not otherwise, then it is termed a contextual anomaly. The notion of the context is induced by the structure of the dataset and has to be specified in the problem formulation. Each data instance is defined using the twp following sets of attributes:
* _Contextual attributes._ The contextual attributes are used to determine the context of the data instance. For example in spatial datasets, the longitude and the latitude, and in time-series time.
* _behavioral attributes._ The behavioral attributes define the noncontextual charachteristics of the instance. E.g. in a timeseries of temperature the temperature itself is a behavioral attribute.

### Collective Anomalies
If a collection of related data instances is anomalous with respect to the entire dataset, it is termed a collective anomaly. The individual data instances in a collective anomaly may not be anomalies by themselves, but their occurrences together as a collection is anomalous.
!!TODO
!!investigate more on collective anomalies[Chandola et al. 2007]

## Anomaly Detection Methods
* [Supervised Method](SupervisedMachineLearning.md), requires pre-labeled data, both normal and anomalous. A typical approach is to build a predictive model for normal vs abnormal classes. Any unseen data instance is compared against the model to determine which class it belongs to. There are two major issues that arise in supervised anomaly detection. First the anomalous instances usually are far fewer than the normal instances in the training data, problem known as [n](Imbalanced Class Distributio.md). Second obtaining accurate and representative labels, especially for the anomaly class is usually challenging. Besides those two issues, the supervised learning detection problem is similar to building predictive models.
* [Semisupervised Method](SemiSupervisedMachineLearning.md), assumes that the training data has labeled instances only for the normal class. Since they do not require labels for the anomaly class, they are more widely applicable than supervised learning.
* [Unsupervised Method](UnsupervisedMachineLearning.md), does not require labeled training data. These techniques make the assumption that normal instances are far more frequent than anomalies in the test data. If this assumption is not true then such techniques suffer from large false alarm rate.

## Anomaly Detection Techniques

### [Classification](Classification.md) Based
Classification is used to learn a model (classifier) from a set of labeled data instances (training) and then, classify a test instance into one of the classes using the learned model (testing). Classification-based anomaly detection techniques operate in a similar two-phase fashion. The training phase learns a classifier using the available labeled training data. The testing phase classifies a test instance as normal or anomalous using the classifier.
Classification-based anomaly detection techniques operate under the following assumption:

_Assumption_. A classifier that can distinguish between normal anomalous classes can be learned in the given feature space.

Based on the labels available during the training phase, classification-based anomaly detection techniques can be grouped into two broad categories:
a) *Multiclass* techniques assume that the training data contains labeled instances of multiple normal classes, and the teach a classifier to distinguish between each normal class and the rest of the classes. A test instance is considered anomalous if it is not classified as normal by any of the classifiers.
b) *One-class* techniques assume that all training samples have only one class label, and they learn a discriminative boundary around the normal instances by using an _one-class classification algorithm_, like one-class SVMs. Below a variety of classification-based techniques are described.

* Neural Network Based. Neural Networks can be applied to anomaly detection in both multiclass and one-class settings. A basic multiclass operates in two steps. First a neural network is trained on the normal training data to learn the different normal classes. Second, each test instance is provided as an input to the neural network. If the network accepts the test input, it is normal and if it [rejects](RejectOptioninClassifiers.md) a test input, it is an anomaly.
  Neural Network [Autoencoders](Autoencoders.md) can also be used for one-class anomaly detection . A neural network with the same number of input and output neurons (corresponding to the features in the data). The training involves compressing data into a lower dimension space. The testing phase involves reconstructing each data instance x,,i,,, using the learned network to obtain a reconstructed output, y,,i,,. The reconstruction error, *e* for the test instance is computed as:
{{$
e_i = 1/n \sum_{j=1}^n (x_{ij} - y_{ij})^2,
 }}$
 where n is the number of features over which the data is defined. The reconstruction score is directly used as an anomaly score for the test instance.

* Bayesian Network Based. [g](Bayesian networks]] can be used for anomaly detection in a multiclass setting. A basic technique for univariate categorical data set using Naive Bayesian network estimates the posterior probability of observing a class label from a set of normal class labels and the anomaly class label, given a test data instance. The likelihood of observing the test instance given a class and the prior on the class probabilities, is estimated from the training dataset. The zero probabilities, especially for the anomaly class, are smoothed using [[Laplace Smoothin.md).
 The basic technique can be generalized to multivariate categorical datasets by aggregating the per-attribute posterior probabilities for each test instance and using the aggregated value to assign a class label to a test instance.

* Support Vector Machines Based. [Support Vector Machines](SupportVectorMachines.md) (SVMs) can be applied to anomaly detection in the one-class setting. Such techniques can be used to learn a region that contains the training data instances (a boundary). Kernels such as _radial basis function (RBF) kernel, can be used to learn complex regions. For each test instance, the basic technique determines if the test instance falls within the learned region. If the instance falls within the learned region then it is declared normal, otherwise it is declared an anomaly.
* Rule Based
TODO!
##### Advantages

##### Disadvantages

### Nearest Neighbor Based
The concept of nearest neighbor analysis can be used for anomaly detection. The basis of the nearest neighbour-based anomaly detection techniques is the assumption that normal instances occur in dense neighborhoods, while anomalies occur far from their closest neighbors.
Neares Neighbor-based anomaly detection techniques can be broadly grouped into two categories:

* k-Nearest Neighbor
A basic k-Nearest neighbor anomaly detection technique is based on the definition of the anomaly score, as the distance of a data instance to its k^th^ nearest neighbor in a given dataset. Then a threshold is applied on the anomaly score to determine if a test instance is normal or anomalous.
* Relative Density
Density Based Anomaly techniques estimate the density of the neighborhoodof each data instance. An instance that lies in a neighborhood with low density is declared to be anomalous while an instance that lies in a dense neighborhood is declared to be normal.

### Clustering Based

### Statistical

#### Parametric
* Gaussian Model Based
* Regression Model Based
* Mixture of Parametric Distributions Based

#### Non-Parametric
* Histogram Based
* Kernel Function Based

### Information Theoretic

### Spectral

## Applications
!!TODO
