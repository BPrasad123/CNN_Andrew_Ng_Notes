# CNN

Finding the vertical edges:  
A 3 * 3 matrix that serves as vertical edge detector is multiplied across the equivalent portion of the image to find the edges.
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Convolution_Edge%20Detection.png)

Horizental edge detector/filter:  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Vertical%20and%20Horizental%20Edge%20Detectors.png)

Other detectors/filters:  
Even back prop can be used to find the weights of the filter for more sophisticated feature extraction.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Other%20Detectors.png) 

## Padding ##
In the both method of edge detection, the image size shrinks with every convolution and critical information is also being lost. To address this issue additional pixel layer is padded on the image pixel matrix that is called padding.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Padding.png)

When padding is not applied then the convolution is called as "valid" convolution and when applied it is called as "same" convolution. Generally the size of the filer is odd as its central pixel captures nice feature.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Padding%20Size.png)

## Strided Convolution ##
Flipping the matrix operation by two positions.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Strided%20Convolution.png)

## Colored Image ##
Pixel matrix of a color image is represented by a 3D matrix corresponding to Red, Green and Blue colors. Hence the filter matrix has to be of 3D as well. The size of the filter matrix is called as channel or depth. Moreover padding can be applied if it is necessary to avoid image shrinkage.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/With%20RGB.png)  

Different filters can be applied for vertical as well as horizental edge detection.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/RGB%20With%20Both%20Vertical%20and%20Horizental%20Convolution.png)  

After multiple filters are applied, the output matrices are combined to represent the convoluted layer. This convolution can be represented as the function of z = w*a + b  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Convolutional%20Layer.png)

The number of parameters depend upon the total number of filters applied and dimension of each filter. It is irrespective of the size of the image on which convolution is applied.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Parameters%20of%20Convolution%20Layer.png)

Summary of Convolution Notations. The order of the dimensions of the input layer might change from one framework to another.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Convolution%20Notations.png)

A series of convolutional steps can be applied to reach a convoluted matrix of desired size. In each step the size of the filter can be changes as per preference. The last output matrix can be flattened as an input to the Nural Network model. Unless padding is applied, generally the size of the image shrinks and the channel size increases with each convolution step.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/ConvNet.png)

There are four steps of convolution network: Convolution, Pooling, Flattening and Fully Connected  

## Pooling ##
Pooling helps to reduce the size and at the same time preserves the feature. Max pooling is one of the pooling approaches that is widely used. Average pooling is also used howevere Max Pooling is considered in most of the cases. Average pooling is sometimes used in very deep NN when it needed to collapse the resprentation of the matrix.  

### Max Pooling ###
The value of filter size and stride size can be changed as well as per preference. Usually for Max pooling, padding is not used. Most commonly used hyperparameters => f =2, s = 2. Since the values of hyperparameters are fixed and there is no back prop, there is nothing to learn for hyperparameter consideration.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Max%20Pooling.png)
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Pooling%20Summary.png)

## Fully Connected Network ##
Once the flattened layer is fully connected with next set of neurons, it layer of neurons is called as fully connected layer. An example is illustrated below.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Fully%20Connected%20Network.png)


## Convolutional Neaural Networks ##
There are a number of networks as illustrated below.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/C%20Networks.png)

AlexNet:  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/AlexNet.png)

VGG 16 Net:  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/VGG.png)
  
## Residual Block ##
A new mechanism was introduced as a short cut to arrive at the intended residual value considering the first residual value along with Z into account in the relu function. This addition of extra layers helped in obtaining better result.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Residual%20Block.png)

With ResNet, Gradient Descent normally converges.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/GD%20with%20ResNet.png)

Why ResNet works?  
With introduction of ResNet layers, when the weights and bias becomes zero with l2 regularization, the added residual value contributes to the next residual value calculation. Padding is applied to ensure same convolution and in case not, a new weight matrix is introduced of appropriate size to ensure the same. It does not hinder the performance however it helps in avoiding some errors.  

![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Why%20ResNet%20works.png)

Same convolution is implemented to keep the dimension constant however wherever pooling is implemented, extra weight layer of appropriate size is added to address the dimension issue.  

![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/ResNet.png)

### 1x1 Convolution (Network in Network Convolution) ###
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/1x1%20Convolution.png)
Use cases:  
It helps to increase or decrease the number of channels while implementing non linearity during the convolution.  

![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/1x1%20Convolution%20use%20case.png)

### Inception Network ###
Apply various filters (convolutions) with various channels however with same convolution with application of padding and striding of 1. Stack the resulted convolutions together.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Motivation%20for%20Inception%20Network.png)

To address the computational power with other filters, 1x1 convolution is impleted to reduce the computation by 1/10 approximately.  
Number of convoluted channel = number of filters  
size of channel of 1x1 = channel of matrix on which convolution is applied  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/1x1%20to%20reduce%20computation.png)

Inception Network:  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Inception%20Module.png)  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Inception%20Network.png)

## Object Detection ##

![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Object%20Classification%20with%20Localization.png)
An object is identified by a few parameters such as presence of the specified object, position of the boundry on the image, size of the boundry, classification of the object. In fact, there can be more such defining parameters as per the need.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Defining%20Target.png)

Object detection:  
Objects can be detected with varying sliding windows. Howevere that is an inefficient way of doing so. Convulutional sliding window is more effective in detecting an object.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Convolution%20implementation%20with%20sliding.png)

Instead of sliding the windows sequencially, with convolution the object can be detected in one go.  
![alt text](https://github.com/BPrasad123/CNN_Andrew_Ng_Notes/blob/master/Notes2/Convolution%20implementation%20with%20sliding%202.png)

