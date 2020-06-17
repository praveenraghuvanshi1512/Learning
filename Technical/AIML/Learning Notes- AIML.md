# Learning Notes

### Topic :  Weight Initialization in Neural Networks: A Journey From the Basics to Kaiming

Date: 09-Dec-2019

Link: https://towardsdatascience.com/weight-initialization-in-neural-networks-a-journey-from-the-basics-to-kaiming-954fb9b47c79

- It’s standard practice when training neural networks to ensure that our inputs’ values are scaled such that they fall inside such a normal distribution with a mean of 0 and a standard deviation of 1.
- To sum it up, if weights are initialized too large, the network won’t learn well. The same happens when weights are initialized too small.

---------------------------

### 18-Jan-2020 : [Deep Learning with PyTorch: Online Workshop Series - Episode 5](https://www.meetup.com/dsnet-blr/events/267531198/)

- Links
  - [Jovian](https://jovian.ml/aakashns/05b-cifar10-resnet)
  - [Colab](https://colab.research.google.com/drive/13gDUjWA28LP8yZZydTkQoTy9vow-KAnp#scrollTo=h-wfooofRoby)
  - aakashns@jovian.ml
  - https://community.jovian.ml
  - https://jovian.ml/aakashns
  - https://jovian.ml/aakashns/05b-cifar10-resnet
- Normalization, In RGB: Red may range from 0.1-0.3, Green may range from 0.7-1.0 and Blue may range from 0.1-0.9. This leads to diverse range, so we need to normalize this range and this is called as Normalization. Normalization will come up with a range that should manage RGB. Mean and standard deviation is used for normalization.
- pin_memory
- 1x1 is used to increase no of channels without mixing the pixels
- Addition : Elementwise addition and Retain channels 
  - l1: (3,32,32) and l2(3,32,32) 
    - l1 + l2 : (3,32,32)
- Concatenation: adds channels 
  - l1: (3,32,32) and l2(3,32,32) 
    - l1 + l2 : (6,32,32) : 6 channels
- Model improvement: Increase data or no of parameters. 1x1 is used to increase no of channels
- data = DataBunch.create(train_ds, valid_ds, bs=batch_size, path='./data/cifar10')
- Certain weights might become large... weight decay helps in that case

