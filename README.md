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
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Early%20Stopping.png)


# Optimization Problems and SOlutions #


## Input Data Normalization ##
Speed of gradient descent also depends upon the distribution of the input data. Normalizing input data makes gradient descent faster. One thing to remember is that the same normalization standards need to be applied to both training and test datasets. With normalized input data, the cost function becomes much easier to optimize.  

## Vanishing/Exploding Gradient Descent ##
Since 'w' is exponentially interpreted for the output calculation, in case of very deep neural network the output value can become very large if the value of 'w' is greater than one and very tiny if 'w' is less than one. Hence accordingly the gradient descent explodes or vanishes.  

![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Gradient%20explodes_vanishes.png)
### Random weight initialization ###
Idea is to randomly assign values to 'w' not so bigger than 1 nor so lesser than 1. For the same it has been observed to assign 1/n (number of input features) as the variance of 'w'. However in case we are using Relu as activation function then 2/n should be assigned. The image below illustrates on the same. This although does not fix the problem fully however it avoids grandient to vanish or explode.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Gradient%20explodes_vanishes%20initialization.png)

### Numerical Approximation ###
Considering two sided difference, the appoximate initialization value of 'w' is much more accurate. Picture below illustrates on the same.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Numerical%20Approximation.png)

### Gradient Checking ###
Gradient checking is one common use case of two sided numerical approximation. Step is to reshape all the parametrs w and b in a vector format say theta. Additing epsilon to left and right of 'w' calculate the theta is changing in form of derivative. Normally 10 to the power '-7' is used as value of epsilon. If the derivative of theta is in the range of the value of epsilon then gradient is all ok otherwise need to debug.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Grad%20Check.png)
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Grad%20Check%20Implementation.png)  


# Optimization Methods #
There are various methods for optimization for Gradient Descent such as Stochastic Gradient Descent, Adam, RMSProp etc. The context here is to breif on all those alogorithms.  
## Mini Batch Gradient Descent ##
When the training dataset is huge, it takes substantial amount of time for the gradient descent to optimize. Hence the training set is devided into some batches and let the gradient descent optimize on each batch at a time in stead of the whole dataset.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Mini%20Batch%20GD.png)  

The cost function is averaged over all the mini batches. Moreover if the regularization is considered then it has to be incorporated while calculating cost function value. Since gadient descent step happens on every batch, hence one epoch sees GD steps equal to number of batches. The entire process needs to be iterated till the grandient converges to its optimum value.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Mini%20Batch%20GD2.png)  


When mini batch size = m, it is same as batch GD. In this case, the GD is slow to converse although it is prone to less noise and GD steps are large. And it is more likely to reach the global minumum at the end.  
When mini batch size = 1, it is called Stochastic GD. In this case, for every training input GD step takes place. It is very noisy and does not converge to the global minimum.  
When mini batch size is greater than 1 and less than m, GD converges fast. If learning rate is kept constant throughout convergence steps then GD does not converge to the global minimum however it wanders around very near to that. Weight decay method tries to reduce the size of the step with each iteration to adress this issue.  
Chossing the size of the batch: If the dataset size is small (approx < 2000) then no need. Typical batch size is power of 2. Hence size can be choosen among 64, 128, 256, 512...Most important part is to ensure that the size of the mini match should fit in the CPU/GPU memory.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Choosing%20mini-batch%20size1.png)  

## Exponentially Weighted Averages ## (One of the other optimization algos better than Gradient Descent)
Considering the temperature example as illustrated in the below image, it tries to decide today's temperature based on weighted averages of temperature from last days and today's observed temperature.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Exponentially%20Weighted%20Average.png)  

Depending upon the value of Beta, the number of past days for average calculation is decided.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Exponentially%20Weighted%20Average%202.png)

It has been observed that in the initial time the curve is close to zero. That is due to the bias and lack of many past observations to make an average of. Hence the formula of Vt is changed to take care of bias at the initial period. The picture below illustrates on the same.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Exponentially%20Weighted%20Average%20Bias%20Correction.png)  

## Gradient Descent with Momentum ## (Another optimization algo that works better than normal Gradient Descent)
In case of gradient descent there are two key considerations to make the GD faster i.e. appropriate learning rate (so that GD does not diverge) and a mechanism that minimizes the vertical learning and increases the horizental learning.  
The concept of "Exponentially Weighted Averages" can be implemented here with updates of 'w' and 'b' for each GD step.  
Pictorially if we observe, the vertical learning steps average out to a value near to zero. Hence the vertical steps get reduced significantly. At the same time since horizental steps are in same direction, the step size stays significant.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/Gradient%20Descent%20Momentum.png)  

## RMSprop ##
It is modified algo of "Exponentially Weighted Averages" to make the learning step faster iun horizental direction and slower in vertical direction. It squares the derivative part while making the learning step. Since the value of horizental step is small and that of vertical step is large, hence the following formula works better. Moreover in this algorithm we can choose larger learning rate without any fear of ending up with divergence. It works with wide range of deep learning architectures.  
![alt text](https://github.com/BPrasad123/ML_DL_Intuitions/blob/master/RMSprop.png)  


## ADAM ## 
Combined version of "Gradient Descent with Momentum" and "RMSprop" to create even better model.  
It works with wide range of deep learning architectures.  

Hyperparameters of Adam to optimize:  
In most of the cases, people do not prefer to optimize beta of momentum or beta of RMSprop or epsilon. Ony thing to optimize is the learing rate.  
