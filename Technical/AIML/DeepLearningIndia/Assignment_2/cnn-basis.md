
Guide: Denny Sam
Mail: itsdennian@gmail.com
Telegram/Whatsapp: 7756851220
[LinkedIn](https://www.linkedin.com/in/itsdennian)

# Understanding Convolutional Neural Networks
1. Basics of opencv
2. ConvNets and Pooling
3. Writing CNN in keras (Building a basic classification model using Keras)
4. AlexNet - Paper Reading
5. Understanding Residual Connections
6. Exploring VGG and ResNets

**Some basics about images**
1. Images are made up of 3 channels (usually) Red, Green and Blue
![1*15yDvGKV47a0nkf5qLKOOQ.png](https://miro.medium.com/max/550/1*15yDvGKV47a0nkf5qLKOOQ.png)
  
2. Each pixel of each channel will have a value between 0 and 255


## Basics of opencv

Open CV is a library used for computer vision. It's not just image manipulation. So initially open CV takes an image and converts it into a numpy array.

**Importing an image**

```python
import cv2
image = cv2.imread("Path/to/image")
cv2.imshow('image', image)

```
Images are imported by default in the BGR format in opencv
So to convert them to RGB format use the following code
```python
rgb_image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
**Resizing an image**
```python
resized_image = cv2.resize(image, (1024, 800))
```

**Cropping an image**
```python
cropped_image = rgb_image[10:500, 30, 800]
```

**Drawing a bounding box in the image**
```python
bounding_box_image = image.copy()
cv2.rectangle(bounding_box_image, (10, 400), (30,343), (0, 300), 10
```

rectangle function takes 4 params 
First - The image itself
Second - Coordinates of top left corner
Third - Coordinates of botton right corner
Fourth - RGB value of the line 
Fifth - Thickness of the line


**Saving an image**
```python
cv2.imwrite("/path/to/export/to.jpg", bounding_box_image)
```

## Convolutional Networks

![1*sX6T0Y4aa3ARh7IBS_sdqw.png](https://miro.medium.com/max/1000/1*sX6T0Y4aa3ARh7IBS_sdqw.png)
_Two layer neural network_

![1*GcI7G-JLAQiEoCON7xFbhg.gif](https://miro.medium.com/max/526/1*GcI7G-JLAQiEoCON7xFbhg.gif)
_Convolutional operation_

[Visualising kernels](http://setosa.io/ev/image-kernels/)

![giphy.gif?w=748](https://ujwlkarn.files.wordpress.com/2016/08/giphy.gif?w=748)
_This is how feature maps look like_

We take 3 3x3 filter and slide it over the complete image and along the way take the dot product between the filter and chunks of the input image. For every dot product taken, the result is a scalar.
![1*Emy_ai48XaOeGDgykLypPg.gif](https://miro.medium.com/max/1000/1*Emy_ai48XaOeGDgykLypPg.gif)

![CNN%203.png?width=500&name=CNN%203.png](https://www.datascience.com/hs-fs/hubfs/CNN%203.png?width=500&name=CNN%203.png)

**Stride**: Number of pixels to shift to right
**Padding**: Keeps the output size same

![1*D47ER7IArwPv69k3O_1nqQ.png](https://miro.medium.com/max/660/1*D47ER7IArwPv69k3O_1nqQ.png)
_Calculate output filter size using this formula_


![1*1VJDP6qDY9-ExTuQVEOlVg.gif](https://miro.medium.com/max/395/1*1VJDP6qDY9-ExTuQVEOlVg.gif)
_Convolution operation with stride length 2 and padding as same_

![main-qimg-fb1cf335af84c4dad4ea25bd8d7e6dd1](https://qph.fs.quoracdn.net/main-qimg-fb1cf335af84c4dad4ea25bd8d7e6dd1)
_What does a CNN learn_

**3x3 Convolutions** : The most common filter size for convolutional operation. The reason being the less number of parameters required for it.
**1x1 Convolutions**: A special kind of convolution introduced to reduce depth of channels.
 
## Pooling
Used to reduce the spatial dimensions of the feature maps. Helps in reducing computation

![1*uoWYsCV5vBU8SHFPAPao-w.gif](https://miro.medium.com/max/396/1*uoWYsCV5vBU8SHFPAPao-w.gif)
_Pooling operation_

**Max Pooling**: Maximum of the values taken
**Average Pooling**: Average of the values taken

![Pooling.gif](https://www.bouvet.no/bouvet-deler/understanding-convolutional-neural-networks-part-1/_/image/e60e56a6-8bcd-4b61-880d-7c621e2cb1d5:bb683ee4bfc6bf29607b1f6926d1bf1274a072b9/full/Pooling.gif)

## Basic architecture of a CNN

![ConvnetDiagram.png](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/Images/ConvnetDiagram.png)


This is how a convolutional architecture network will look like
1. The input passes through the first convolutional filters to create multiple feature maps. Feature maps are representations the filters learnt from the image.
2. The feature maps are then passed through pooling layers which reduce the size of the maps.
3. The output of the pooling layers are passed through a non-linear activation function, mostly ReLU
4. Steps 1, 2 and 3 are considered to be a block which are repeated multiple times. The parameters such as number of filters, filter size etc. vary from block to block
5. After computing the feature maps, the output is then passed to a fully connected layer, which is then fed to a softmax function. 
6. The softmax function compresses the values it got from the fully connected layer between 0 and 1. You specify the output of the softmax function as the number of classes you need as output. Softmax function will output the probabilities of each class. 

![maxresdefault.jpg](https://i.ytimg.com/vi/o6HrH2EMD-w/maxresdefault.jpg)
_Softmax function_

## Let's build a classifier!

We will be using MNIST dataset 


## Paper reading: [AlexNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)

**Takeaways**
1. Used non saturating non linearities. f is non-saturating iff (|lim𝑧→−∞𝑓(𝑧)|=+∞)∨(|lim𝑧→+∞𝑓(𝑧)|=+∞). Sigmoid and Tanh are saturating non-linearities because there's a saturation point for the activations in it. After a point it's not possible for the activations to go any further. 

Sigmoid:
![sigmoid.jpeg](http://cs231n.github.io/assets/nn1/sigmoid.jpeg)

Tanh:
![tanh.jpeg](http://cs231n.github.io/assets/nn1/tanh.jpeg)

ReLU:
![relu.jpeg](http://cs231n.github.io/assets/nn1/relu.jpeg)

2. Alexnet contains 8 layers; 5 convolutional layers and 3 fully connected layers.
3. Implemented an optimized 2D convolution algorithm where one GPU convolves over the top of the image while the other GPU runs on the bottom.
4. Kernels of layer 3 take all input maps from layer 2 but kernels of layer 4 only take input maps from the same gpu.
5. They have used overlapping pooling in their implementation which they say has led to a slightly better accuracy.
6. Dropout creates multiple architectures. Combining output of multiple architectures is a great way of improving accuracy


## VGGNet

![convolutional-neural-network-models-deep-learning-50-638.jpg?cb=1500039867](https://image.slidesharecdn.com/cnnmodels-170714134232/95/convolutional-neural-network-models-deep-learning-50-638.jpg?cb=1500039867)

- Simple architecture. Introduced 'Deeper networks are better' concept
- Introduced the idea that multiple small filters are better than a single large filter when both have same receptive field areas on the input image.

1 layer of 7x7 = 49 parameters
3 layers of 3x3 = 27 parameters

- Pooling 2x2 with a stride of 2
- Multiscale training was used


## Understanding Residual connections

![1*D0F3UitQ2l5Q0Ak-tjEdJg.png](https://miro.medium.com/max/1140/1*D0F3UitQ2l5Q0Ak-tjEdJg.png)
_Skip or residual connection_


- Residual connections are not specific to CNNs. It's just popularised by ResNet hence used more in vision based approaches.
- Deeper networks are good for learning more features but as the networks get deeper, their ability to learn simple functions, like identity functions, go down. 


![we-need-to-go-deeper-21752911.png](https://pics.me.me/we-need-to-go-deeper-21752911.png)


- This is evident from the fact that as you keep on adding layers, we see a degradation in accuracy.


![Screenshot 2019-09-21 at 08.47.52.png](:storage/251124fe-a7d2-4060-b979-478bb8a4c00a/e70e4e8c.png)


- To counter this, we add skip connections. How a skip connection looks like is shown above. Skip connections help in learning identity functions by itself.

`R(x) = Output — Input = H(x) — x` 

R(x) is called the residual

`H(x) = R(x) + x`

From the diagram above we can see that the since x is learnt via the skip connections, the layers are learning the residuals, not the original output.

## ResNet

![1*6hF97Upuqg_LdsqWY6n_wg.png](https://miro.medium.com/max/3048/1*6hF97Upuqg_LdsqWY6n_wg.png)

- Resnet has a bunch of residual blocks which leads to a larger network with 152 layers. It beats human level performance on ImageNet
- While training, some of the residual blocks can skip their training, some of them can train less. Some parts of the network gets trained for some samples. Some parts gets trained at different rates.
- Since we don't know the optimal number of layers required to get a good accuracy, ResNets can be seen as an ensemble technique which does something like an architectural search. It skips the layers that doesn't add to the accuracy. 


## Assignment

1. Read the [densenet paper](https://arxiv.org/abs/1608.06993) and implement the architecture in Keras
2. Use this architecture to train CIFAR-10 dataset. 
3. Accuracy expectations: above 85%

You can submit your assignments till Sep 30, 2300 Hours









