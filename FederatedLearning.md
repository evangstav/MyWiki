# Federated Learning

## Differential Privacy

### Introduction
The general goal of differatial privacy is to ensure that different kinds of statistical analysis don't compromise privacy. But what is privacy?
*Privacy* is preserved if, after the analysis, the analyzer doesn't know anythin about the people in the dataset. They remain "unobserved".
This is an inadequate definition for our context (ML).

The main idea is that we are no trying to protect data we are trying to protect people.
A good definition is given by Cynthia Dwork, in Algorithmic Foundation of DP as: "Differential Privacy" describes a promise, made by a data holder, or curator, to a data subject, and the promise is like this:
"You will not be affected, adveresely or otherwise, y allowing your data to be used in any study or analysis, no matter what other studies, data sets, or information sources, are available"

### Goal
* Most accurate prediction with the greatest amount of privacy
* Greatest fit with trust models in the actual world(don't waste trust) -> flexible strategies

### Can we anonymize data?
Just anonymizing data is insufficient as it has been shown multiple times. By using multiple different anonymized datasets, researchers have been [able to deanonymize large proportion of the participants, using statistical techniques](https://www.cs.utexas.edu/~shmat/shmat_oak08netflix.pdf).

### Sensitivity(L1 Sensitivity)
The maximum amount that the query changes when removing an individual from the databse. Used to compare how much information queries are leaking.

### Differencing Attack

### Types of Differential Privacy(DP)
One strategy to protect peoples privacy is by adding random noise, both to the databases and to the queries.
There are two kinds of DP, which refer to the place of adding noise, _locally_ or _globaly_.
1. Local DP: Adds noises to each individual data point. Another way to think of it is ass adding noise to the database itself. In this setting users are most protected
2. Global DP: Adds noise to the function(query) outputs.

If the db owner(_trusted curator_) is trustworthy then the level of protection is the same, but global DP leads to more accurate results, with the same level of privacy protection.

### Local DP
In local DP, given a collection of individuals, every individual adds noise to his data input before sending it to the DP. So how much noise should we add?
*Plausible Deniability*
