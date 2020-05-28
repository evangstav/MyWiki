# Channel Charting

## Main Objective

The main objective of CC is to learn a low-dimensional embedding, the so called _channel chart_, from a large amount of high-dimensional CSI of transmitters (e.g. mobile or fixed UEs) at different spatial locations over time. This channel chart _locally_ preserves the original spatial geometry, i.e., transmitters that are nearby in real space will be placed nearby in the low-dimensional channel chart and vice versa. CC will learn whether two transmitters are close to each other by forming a [|_dissimilarity measure_](.md) between CSI features of these transmitters. Based on this, CC generates the low dimensional chart in an uspervised fashion from CSI only and without assumptions on the physical channel, i.e., whihout the aid of information from GNSS, such as GPS, triangulation techniques or fingerprint-based localization methods.
This important property enables CC to extract geometry information about the transmitters in a completely passive manner, opening up a broad range of novel applications.

## Papers

1) Channel Charting: Locating Users within the Radio Environment using Channel State Information.

*Key Terms*

CSI: Channel State Information
BS: Base Station
UEs: User Equipments

*Central Ideas*
To effectively manage and optimize new tech future systems must lean on the availability of large amounts of high dimensional CSI acquired at a multi-antenna base station over large bandwidths and at fast rates, and from a large number of UEs. To _effectively_ use the collected CSI, the network has to learn the radion geometry in which the UEs are moving. What needs to be learned is a chart of the network radio geometry, which represents UE location and velocity information related to CSI. In order to automate functions, dynamically adapt o changes in the environment, and avoid human intervention for training, learning the radio geometry should be ubsupervised.

*Radio Geometry*

*Channel Fingerprinting*
- Fully Supervised

[g](*Manifold Learning.md)*

[n](*Dimensionality Reduction.md)*

[g](*Multidimensional scaling.md)*

[*](*Sammon's Mapping.md)


