# Channel Charting Special Course

== Theory == 

== [ ](Implementation Notes.md)==
## Principles

### Main objective
The main objective of CC is to learn a low-dimensional *embeding*, the so called channel chart, from a large amount of CSI (Channel State Information) of transmitters at different spatial locations over time. This channel-chart _locally_ preservers the original spatial geometry, i.e. transmitters that are nearby in real space will be placed nearby in the low dim chart and vice-vera. CC will learn whether two transmitters are close to each other by forming a [e](dissimilarity measur.md) between CSI features of these transmitters. 
Based on this, CC generates in an usupervised way from CSI only without assumptions on the physical channel or any other information from localization techniques (GPS, triangulation etc.). This important property enables CC to extract geometry information about the trasmitters in a completely passive maner, opening up a broad range of novel applications.

### Operating Principles
#### Overview
Mobile transmitters Tx at spatial locations *X* are sending information to a multi-antenna receiver Rx over the wireless channel _H_. CC first users CSI *h* to extract features *f*, which are the processed by a channel charting algorithm to learn forward charting function _C_ that generates an embedding inspatial geometry z that preserves local geometry in an unsupervised manner.

#### Channel Function

W are not interested in the transmitted data, but in the associated CSI. Concretely the Rx uses the received data $y_n$ where $ n = 1,...,N $ time instants, to extract CSI denoted by the vector $ h_n \in C^M  $ where M denoted the dimensionality of the acquired CSI. The generated CSI typically describes angle-of-arrival, power delay profile, Doppler shifts, RSS, signal phase, or simply first and seconf moments (e.g. mean and covariance) of the received data. Typically we have M >> D where D the spatial dimensionality. We denote the mapping from spatial location $x_n$ to CSI $ h_n $ with the following channel function, 
{{$
H : R^D \to C^m 
}}$

where $C^m$ refers to the _radio geometry_. 

#### Channel Charting
*Key Assumption*: We assume that the statistical properties of the mlti-antenna channel vary relatively slowly across space, on a length-scale related to the macroscopic distances between scatterers in the channel, not on the small fading length-sccale of wavelengths. We furthermore assume the channel function _H_ to be static.

Channel Charting comprised of two _"parts"_. 
1) feature extraction
2) forward charting function

CC starts by distilling the CSI vector $h_n$ into suitable channel features. We denote the features extraction phase by the function:
{{$
F: C^M \to C^{M'}
}}$
Feature extraction serves three purposes:
i) extracting large-scale fading properties from CSI,
ii) distilling CSI into usefull information for the subsequent pipeline
iii) reducing the vast amount of channel data.

CC then proceeds by using the set of N collected features to learn the _forward charting function_ (with possible side info) in an unsupervised manner. We denote the forward charting function to be learned by:
{{$
f_c : C^{M'} \to R^{D'}
}}$
which maps each channel feature *f,,n,,* to a point *z,,n,,* $ \in R^{D'} $ in the low dimensional channel chart. Typically we have D = D'. The objective for learning f,,c,, is as follows:

* The forward charting function f,,c,, should preserve local geometry between data points, i.e. it should satisfy the following condition:
{{$
d_z(z, z') \approx d_z(x, x'), where
x, x' \in R^D are two points in the real space within a certain neighborhood
and z, z' \in R^D' are the corresponding vectors in the learned channel chart.
}}$
the functions d_x, d_z are suitable defines measures of distance (or, more generally, dissimilarity) andthe neighborhood size depends on the physical channel.

=== Involved Geometries and Usage of CC===
Transmitters (Tx) are located in Spatial geometry R^D^ .
Receiverers (Rc) extract channel information (CSI) in radio geometry C^M^.
Feature extraction distilles usefull information into feature geometry C^M'^
Forward charting function maps features into a low dimensional channel map in R^D'^, preserving local geometry.

## Quality Measures
To characterize the usefullness of the generated channel charts, we nee a measure of how well the channel features or poits preserve the spatial geomtry of the true transmitter locations.

To asses the CC quality we use two metrics borrowed from dimensionality reduction methods, namely _continuity_ and _trustworthiness_
A) Continuity (CT):
    A)   
B) Trustworthiness (TW):
    A) 

## Channel Features

## Channel Charting Algorithms

## Siamese Neural Networks

1) Sammon's Mapping:: Sammons mapping takes a dataset *X* of *N* vectors of dimension *D* and maps all vectors to a set *y* in some *D'* dimensional space, where typically *D'* << *D*. The goal of _Sammon's_ mapping is to preserve small pairwise distances between the high- and low-dimensional vectors by minimizing the following loss function:
{{$
L(Y) = \sum_{n=1}^{N-1}\sum_{m=n+1}^{N}w_{nm}(|x_n-x_m|-|y_n-y_m|)^2.
}}$
The parameters w,,nm,, are used to de-weight the importance of pairs of vectors that are dissimilar in high dimensional space. The common choise for _Sammon's mapping_ is 
{{$
w_{mn} = |x_n - x_m|^{-1} for n \neq m
}}$
1) Siamese Networks for Parametric Sammon's mapping:: 
2) Supervised and Semisupervised Extensions


# Possible Extensions
Variational Siamese???
Ouput mean+std for each dimension sort of like a probability sphere!





