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


## Why does Regularization solve overfitting or high variance problem? ##
Higher value of regularization parameter (lambda) makes the value of w tend to zero. Hence lessens the effect of some of the hidden nodes and thus makes the function more linear and reduces the variance. Below picture (taken from Prof. Andrew Ng's DL course) illustrates the purpose here.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Bias%20and%20Variance.png)

When higher value of lamda reduces the value of w, that in turn reduces the value of z as well. Smaller size of z make the curve roughly linear that corresponds to one hidden layer. In same way, other hidden layers also get roughly linear and that reduces the variance and overfitting. A point to be noted that the revised cost function with the inclusion of regularization should be considered all the time. Otherwise it will not serve the purpose. Picture below taken from Prof. Andrew Ng's DL course for illustration.
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Regularization.png)  

## Dropout Regularization ##
In NN, randomly drop some nodes or make them inactive for each training example. This results in smaller and diminished network to reduce the noise. For implementation there are three apporaches however the most common one is "Inverted Dropout".  
"Keep-prob" is a hyper-parameter that denotes the percentage of active nodes in a given layer. If it is 0.8 then 80% of nodes will be active and remaining 20% will be shut off randomly for each training example or iteration of gradient discent. In the illustraion below d3 is the bullian array to implement node shut off randomly. With this drop out the value of 'a' is also reduced and than in turn reduces the value of 'z' as well and that is not correct. Hence at each iteration value of 'a' is further devided by 0.8 (the value of keep-prob) as if all the nodes actively contributed.  
Remember that drop out should not be implemented when running NN on test data as we do not want our output to be random.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Dropout%20Intuition.png)

## Why dropout works ##
In NN, implementation of dropout makes the weights shrink just in a similar way as l2 regularization. This addresses the variance issue.
keep-prob parameter value can be assigned differently for different layer depending upon the number and size of the layer. With drop out there is no well defined J function anymore hence for all other checks related to grandient discent, it is advised to check the NN model without dropout first and once everything is ok implement dropout for regularization. Most importantly regularization should be implemented only overfitting issue occurs.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Why%20dropout%20works.png)

## Other methods of Regularization ##
### Image Augmentation ###
At times getting more training data is expensive. Hence in case of image processing, Image augmentation is another solution!!  

### Early Stopping ###
As we are aware 'w' is randomly assigned with a very small number close to zero. As the model is trained more and more the value of 'w' also increases. Now, when we compare the loss function on training dataset against that on the Dev set (CV), we see that the loss function in both the cases continue to converge along however at a certain point the loss function on the Dev set starts diversing. We can stop the model there itself. At that point the value of 'w' is mid sized and the trained model did not pick up much noise. However it has a downside :  
Ideally optimization of cost function and regularization for overfitting issue should not be addressed simultaneously. However with early stopping it tries to do both the things which may not be an accepted case in many cases.

