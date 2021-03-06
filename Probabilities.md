= Probabilities = 

## The likelihood function
- Imagine you have N datapoints
- We assume it follows some parametric distribution(e.g. Gaussian)
- How can you determine these parameters?
- The likelihood function, should be:
{{$
L(\Theta) = \Pi_{i}^{N}p(x_{i}|\theta)
}}$
- Notice it is the joint distribution of all independent data points
- For the case of the Gausian, 
{{$
\theta = {m,\sigma}
}}$
- So the likelihood function, would be:
{{$
L(\theta) = \Pi_{i}^{N}* e^{-(x_{i} - m)^{2}/2*\sigma^{2}}/\sqrt{2*\pi*\sigma}
}}$
- If we actually had the true parameters this likelihood would have the maximum value.
- So this becomes an optimizstion problem of finding the best values of $\theta$ that maximize the function $L(\theta)$.

## The log-likelihood function
- For practical reason we apply a logarithmic transformation to the likelihood function because:
    - Less prone to numeric error (numerical stability)
    - Computationally faster
    - Applying log to prodcuts makes them sums. Much easier to compute sums than products.

## Maximum likelihood estimate
- The maximum likelihood estimate is the value of the parameter that maximizes the log-likelihood
- In the case of gaussian the MLE corresponds to:
    1) the sample mean
    2) the sample variance
- The fact that we an MLE it doesn't mean that we have a good model.


## Bayesian vs Frequentists

### Two kinds of uncertainty

Philosofically there are two types of uncertainty, one due to lack of knowledge called *epistemic*, and one about inherent randomness called *aleatory*.

### Two kinds of probability

1) Frequency definition:: Probability represents the long  term frequency with which a given event occurs, if it repeated infinite times.
2) Bayesian definition:: Probability represents a degree of belief in the truthof a given proposition.
