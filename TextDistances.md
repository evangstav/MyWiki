# Text Distances


## Hamming Distance
The ~~Haming Distance~~ compares every letter of the two strings based on position. So the first letter of word 1 is compared to the first letter of word 2 etc.

### Advantages:
* Position-wise comparison is very fast and simple

### Disadvantages
* strings should have equal number of characters


## Levenshtein Distance
The Levenshtein distance is the number of operations needed to convert one string into another. So every edit needed will add 1 to the Levenshtein distance.
There are 3 types of operations:
* Inserting a character
* Deleting a character
* Substitute a character with another

### Advantages
* More intuitive

### Disadvantages
* Less simple but still simple enough
* Takes a bit longer to compute


## Cosine Distance
Cosine distance (or Cosine Similarity) considers the distance between documents. To compute the Cosine Similarity you need to perform the following steps:
1) Get all unique words of your combined text documents.
2) [|Make a vector for each document](Vectorizing Text.md)
3) Compute Cosine Similarity (Distance is 1-Similarity). Similarity is computed by computing the dot product of 2 vectors *a* and *b* divided by the product of their norms *|a|*, *|b|* as, 
{{$ 
\text{similarity} 
= 
\cos{x}  
= 
\frac{A \dot b}{\|A\| \|B\|}
}}$
, where similarity is a number between 0 and 1.
