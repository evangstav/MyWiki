# Sequential Data

Stationary Sequential Distributions::
Data evolves over time but the distribution, from which it is generated remains the same.

Non Stationary Sequential Distribution::
The generative distribution itself evolves over time.

## Markov Models
We assume that future predictions are independent of all but the most recent observations. These models are tractable but also farely limited. We can obtain amore general framework while retaining tractability, by introducing latent variables, leading to state-space models. 

### Markov Chain Order
How many previous observations affect the current observation. For example, in second oder markov chain, observations {x_n}, in which the distribution p(x_n|x_(n-1),(x_n-2)) is conditioned on the value of the previous observation x_(n-1) and x_(n-2). Similarly for M-order.

For continuous variables, we can use linear-Gaussian conditions distributions in  which each node has a Gaussian distribution whose mean is a linear function of its parents. This is known as an autoregressive or AR model. 


= [ ](Hidden Markov Models.md)=

