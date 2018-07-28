# Goal #

There are numerous reads for ML and DL fundamental aspects. The goal here is to touch upon all the elementary and important ones with simple and short explanation in plain english so that it will help us to remember all that by taking a quick look at this page.  

## Over-Fitting ##
When a model performs very well on the training dataset giving very less error however it throws comparably much more error while tested on test dataset, that model is called as overfitted one.
Why over-fitting happens: Essentially in the context of Machine Learning, all the input data has two components - Pattern and Stochastic Noise. The goal is to train the model on the patter avoiding noise. However when the model fits the noise then it becomes very specific to that corresponding training entry and it gives overfitting result.  
Solution: One of the solutions is to introduce regularization by penalyzing the model on picking the noise data. On the other hand more training data can be added.
