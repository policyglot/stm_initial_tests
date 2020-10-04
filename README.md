# stm_initial_tests
Initial explorations on using the STM module in R so as to later add the stm feature into gensim

## Statistical Understanding
The approach used by the authors is a partially collapsed variational Expectation-Maximization algorithm which upon convergence gives us
estimates of the model parameters. Our approach is to posit a hierarchical mixed membership model for an-
alyzing topical content of documents, in which mixing weights are parameterized by
observed covariates. In this model, topical prevalence and topical content are spec-
ified as a simple generalized linear model on an arbitrary number of document-level
covariates, such as news source and time of release, enabling researchers to introduce
elements of the experimental design that informed document collection into the model,
within a generally applicable framework.

Specifically, for topic prevalence, the Dirichlet distribution that controls
the proportion of words in a document attributable to the different topics is replaced with a
logistic Normal distribution with a mean vector parametrized as a function of the covariates

The core of the model posits a the document-level 'attention' (proportion allocated) to each topic from a logistic-normal generalized
linear model based on a vector of document covariates $X_d$.


Regularizing prior distributions are used for γ, κ, and (optionally) , for the following reasond:
1) To enhance interpretation and 
2) Prevent overfitting.

## Intractbable Posterior for Topic Content
For topical content, we define the distribution over the terms associated with the different topics as an exponential family model, similar to a multinomial logistic regression, parametrized as a function of the marginal frequency of occurrence deviations
for each term, and of deviations from it that are specific to topics, covariates and their interactions.

As with other topic models, the exact posterior for the proposed model is intractable, and suffers from identifiability issues in theory (Airoldi et al. 2014a). Inference is further complicated in our setting by the non-conjugacy of the logistic Normal with the multinomial
likelihood. 

We develop a partially collapsed variational Expectation-Maximization algorithm that uses a Laplace approximation to the non-conjugate portion of the model

