# Goal #

There are numerous reads for ML and DL fundamental aspects. The goal here is to touch upon all the elementary and important ones with simple and short explanation in plain english so that it will help us to remember all that by taking a quick look at this page.  

## Over-Fitting ##
When a model performs very well on the training dataset giving very less error however it throws comparably much more error while tested on test dataset, that model is called as overfitted one. It is due to high variance problem in the training data.
Why over-fitting happens: Essentially in the context of Machine Learning, all the input data has two components - Pattern and Stochastic Noise. The goal is to train the model on the patter avoiding noise. However when the model fits the noise then it becomes very specific to that corresponding training entry and it gives overfitting result.  
Solution: One of the solutions is to introduce regularization by penalysing the parameters of the model on picking the noise data. On the other hand more training data can be added to address the high variance issue.  

More reads: https://www.quora.com/What-is-regularization-in-machine-learning  

## Regularization ##
Considering an example of logistic regression, let us explain both types of existing regularization methods. Idea is to penalyse both the paramters w and b. However since b is constant, we can avoid penalysing b.  
l2 regularization: Adding penality at the square of the parameter w  
l1 regularization: Adding penality at the mod of w. This indroduces sparse hence it shrinks the model. Unless otherwise it is really needed it is considered to be better to l2 regularization.  
In both the cases, lambda is the regularization hyper-parameter that is used and that needs to be tunes as well for optimization.  
In case of Neural Network, similarly penality is added at the square of w at the hidden layer level. That is called Frobenius regularization. Now that regularization is added, it needs to considered while calculating the back propogation. Because of the addition of Frobenius regularization (similar to l2 regularization), the value of w is decreased relatively smaller in each back prop step. That is why this regularization is also called as "weight decay"  


## Why does Regularization solves overfitting or solves high variance problem ##
