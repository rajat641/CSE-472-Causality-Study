
#### First, we need to understand the meaning of Causality and difference between Causality and Correlation.
I read this very interesting definition of Causality and Correaltion:
* Correlation - Diaper sales increases with Beer sales on weekends
* Causation - Babies need beer on weekends.

There is a very good and simple youtube video on this concept. Here is the [Link](https://www.youtube.com/watch?v=ROpbdO-gRUo) .

# Causality-Study
Our task was to find which part (e.g., a word, phrase, or an aspect of a restaurant) of the review written by a user is causally related to the rating she/he gives using the Yelp online reviews data, and estimate the causal effects. 
We have used causal inference methods and  natural language processing models on Yelp data.

# Multi Aspect Sentiment Analysis
In order to extract sentiments for each aspect in the reviews, we
used the NLP approach outlined by @pmin [2]. This approach uses Neural
Coreference offered by the spacy library in addition to multi-label Naive
Bayes classification in scikit learn. First, the pronouns in the text are
replaced by the actual subjects using coreference. At this point, for each
sentence we can identify the subject. The training data by @pmin includes
labels for subjects relating to food, service, price, ambience and misc. The
sentiment for each narrative is extracted by using word2vec model trained
on the Google News dataset. Since we have an aspect related to each
narrative and a sentiment related to the narrative, we can derive the
sentiment related to each aspect.

# Confounders
The second step of our framework is to find the confounders for
each aspect(and the effect). For this we used the deconfounder model[3].
This model uses probabilistic inference to find the latent confounders. The
approach is very similar to LDA.
For our analysis we used ratings and popularity as the effects while
using the aspect sentiments as the causes. In addition we also split the
data into spatial clusters to examine the effects of spatial heterogeneity
on the confounders. In order to achieve this we used agglomerative
clustering with the ward method. This method tried to optimize the
hierarchy such that the L2 norm between the nodes in each cluster is
minimized.In order for the deconfounder to produce inference results, it needs
a sufficient number of examples. Thus, we set a threshold of 100 for each
cluster in our hierarchy and calculated the latent confounders for each
cluster. The cluster at the top of the hierarchy represents the confounders
for the entire toronto dataset, while the smallest clusters represent the
latent confounders for ~100 spatially colocated nodes.
### The idea of using confounder variables is taken from here https://www.microsoft.com/en-us/research/video/the-blessings-of-multiple-causes/

# Results
The observations and final result can be found here: [CSE –472 Project _Report .pdf](https://github.com/rajat641/CMS-CSE324-WebProgramming/files/4026496/CSE.472.Project._Report.pdf)



# References and Citations
1. http://www.ucdenver.edu/academics/colleges/PublicHealth/resourcesfor/Faculty/perraillon/perraillonteaching/Documents/week%203%20causal.pdf
2. https://medium.com/@pmin91/aspect-based-opinion-mining-nlp-with-python-a53eb4752800
3. https://arxiv.org/pdf/1805.06826.pdf
4. https://colab.research.google.com/github/blei-lab/deconfounder_tutorial/blob/master/deconfounder_tutorial.ipynb#scrollTo=7Ps8ev0rw1km
5. https://amplitude.com/blog/2017/01/19/causation-correlation


# Install Dependencies
`pip install -r requirements.txt`

# Run

`jupyter notebook SpatialDeconfounder.ipynb`

