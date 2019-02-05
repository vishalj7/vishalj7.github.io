---
layout: post
title: Convolutional Neural Network
tags: Machine-Learning CNN Image-Recognition Convolutional-Neural-Network
---



### Convolutional Neural Network

#### What is Convolutional Neural Network (CNN)?

Convolutional Neural Network is a neural network which is primarily used for classifying images such as determining whether an object exists within the image. They have been used to identify road signs, people's faces and even determining handwriting. CNNs can be used in Natural Language Processing (NLP) and even speech recognition. 

CNNs differ from ordinary neural networks as CNNs try to find patterns within the image and comparing this to an ordinary neural network which have features and when testing CNNs try to find the same pattern from the training set where as ordinary neural networks try to use the features. 

CNNs can't actually see the image so how does it determine whether 2 images are of the same subject i.e. a picture of a dog.

Well, the computer can't see colour, texture, brightness etc. but it can understand numbers so what happens is that the image is translated into numbers.


#### How does it work?

There are 4 steps within CNN :


#### Convolution 

A small convolution filter (a small grid) called the kernel moves from the left to the right of the image moving across the pixels in the image. The moves depend on the number of strides that can be set which I will talk about in the next section. The kernel fits over a number of pixels and this grid can be defined and the dot product of the input values (number from all the pixels that the kernel fits over) is calculated. This calculation is then added to a feature map. Once the feature map is completed then we can move on to another filter using the same process. A kernel has a specific height and width, like 3x3 or 5x5, and by design it covers the entire depth of its input so it needs to be 3D as well.


![an image alt text]({{ site.baseurl }}/images/cnn_kernal.gif "Convolution step - How the Kernel moves across each pixel in the image.")

The blue grid is the input image and the green grid that is moving left to right is the kernel and finally the dot product is calculated and then added to the feature map ( the grid on the right). 

This is one step in a 2D operation and realistically the input would be in 3D to include height, width and depth (depth of colour RBG). This is just using one filter to generate a feature map but in practice we will be using lots of different filters to generate lots of feature which are then put together to create the final output of this convolution layer. The depth of the kernel matches the depth of the input image so that everything from the input image is covered. 



#### Non Linearity (ReLU)

Rectified Linear Unit is considered as part of the convolution step and it is a type of activation function. The reason why we use this relu activation function is to increase non-linearity in the images. Images naturally contain a lot of non-linear features such as colour, borders and when we use pass the image through the convolution stage the image area selected can become linear as we are only working with a very small area and the chances of the same colour being present is high. So using the relu activiation function will increase the non-linearity as it removes all the black elements from it, keeping only those carrying a positive value.  



#### Stride and Padding 

This is not really a step but information The stride is a number that is used to specifiy how many pixels for the kernal to move by when the it finishes the calculations on the current set of pixels. The default is 1 and this usually involves the kernel overlapping and covering some pixels more than others. 

![an image alt text]({{ site.baseurl }}/images/cnn_stride.gif "Convolution step - Stride 1 moves across each pixel in the image.")

Now increasing the stride size, means less calculations and computation but also a smaller feature map so at each layer the feature map would be getting smaller. 

![an image alt text]({{ site.baseurl }}/images/cnn_stride2.gif "Convolution step - Stride 2 moves across each pixel in the image.")

Padding is used by to keep the feature map (height and width) the same size as the input image by adding 0 values around the input image.  

![an image alt text]({{ site.baseurl }}/images/cnn_padding.gif "Convolution step - Padding allows the feature map to remain the same size.")



#### Max Pooling 

Pooling often used in the CNN and its purpose is to reduce dimensionality which in turns reduces the number of outputs and also results in less computation. This is a type of down-sampling where it is applied after the feature maps have been created so after the convolution step. The input is the feature map from the convolution step and a grid (similar to the kernel) is passed over the feature map where a value is selected based on the pooling type max, sum, or mean. This allows the pattern to be detected as it is removing unnecssary information and accounts for distortion. As a result of this a smaller feature map is created as well as the number of parameters. This reduces the chance of overfitting from occurring.

The other reason why pooling is important is that no matter where the pattern you are trying to find is (centre, top corner etc), or at what angle it is, the aim is for the CNN is able to identify it. 



#### Classification (Fully Connected Layer)

This is the final step of creating a CNN and the outputs from the convolution and pooling layer is used as the inouts for this step but before they can be used they need to be flattened as the output of convolution and pooling layer are in 3D whereas the fully connected layer expects a 1D of vector numbers. Flattening converts the outputs from convolution and pooling layer conver the grid into a 1d list of vector numbers.  

In this step there are 3 main components:
    + Input layer 
    + Fully Connected layer
    + Output layer (Classification layer)

![an image alt text]({{ site.baseurl }}/images/cnn_fully_connected.png "Fully Connected layer.")


#### Input layer

As mentioned above the input layer is the output from the convolution and pooling layer but as a 1D vector.


#### Fully Connected layer

From the above picture each circle is a neuron and each neuron in the previous layer is connected to each neuron in the next layer. The connections between 2 neurons carry a weight and this allows the whole input to be connected. This layer is where features are detected such as big nose or whiskers when trying to classify whether an image contains a cat or dog. 


#### Classification layer

The final layer will contain a number of classifications based on your CNN and the features detected will be passed to this layer. All the possible classes for this layer will return a probability that it contains that class e.g. that it is a dog or cat. 

![an image alt text]({{ site.baseurl }}/images/cnn_classification.png "Classification Layer")


Below is the full architecture that I talked about above:

![an image alt text]({{ site.baseurl }}/images/cnn_architecture.jpg "The whole architecture end to end.") 