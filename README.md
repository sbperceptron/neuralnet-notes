# Neuralnet-notes
notes on neuralnetworks

# Alexnet
1. 5 conv layers (filtersizes 11,5,3,3,3)
2. 3 fully conected layers
3. relu activations
4. dropout layer after fully conected layer

# 1. Dropout layers 
  Due to dropout layer, different sets of neurons are switched off, represent 
different architecture and all these different architectures are trained
in parallel with weight given to each subset and the summation of weights 
being one . For n neurons attached to dropout , the number of subset architectires 
formes is 2^n. so it amounts to prediction being averaged over these ensembles 
of models. this provides a structured model regularization which helps avoiding 
the over fitting. Amother view of DropOut being helpful is that since 
neurons are randomly chosen, they tend to avoid developing co adaptationd 
among themselves thereby enabling them to develop meamningful features, 
independent of others.

# VGG 16
  Multiple small sized kernels are better than the one with single large 
sized kernel because multiple non lineat layers increases the depth of 
the network which enables it to learn more complix features, and that to a
at a lower cost. Also 3*3 ketnels help in retaining finer level properties of image

  eg: 3 3*3 conv filters have 3*9C^2 parameters and a single 7*7 filter will have
49C^2 parameters

!["VGG16 Architecture"](https://github.com/sbperceptron/neuralnet-notes/blob/master/VGGNet.png)

  The vgg convolutional layers are followed by 3 fully connected layers.

# GoogleNet/inception:
  Best performance on image net, but deployement onto most modern gpu is a problem 
because of huge computational requirements, both in terms of memory and time. 
it is inefficient due to large width of convolutional layers. In vgg cinv operation 
every output channel is connected to every input channel and so it is called dense 
connection architecture.

  *" Most of the activations in a deep network are either unnecessaary ot redundant
  *because of correlations between them."

  Therefore the most efficient architecture of a deep network will have a sparse 
connection between the activations, which impies that all output channels will
not have a cinnection with all input channels. there are techniques to prune 
out such connections which would result in asparse weight connection. But kernels 
for sparse matrix multiplication are not optimized in cuda for GPU.

  So google net devised a module called inception module that approximates a sparse 
CNN with a normal dense construction. Also, it uses convolutions of different sizes 
to capture details at varied scales 

  Another salient point about the module is that it has a so called bottleneck layer 
. It helps in the massive reduction of the computation requirement.

  Another change that Google net made, was to replace fc layers at the wnd with a 
simple global average pooling after the last convloutional layer. This drastically
reduces the total number of parameters without reducing the accuracy.

!["inception module"](https://github.com/sbperceptron/neuralnet-notes/blob/master/inception_module.png)

Examples: YOLO neural network
!["YOLOV2"](https://pjreddie.com/media/files/papers/YOLO9000.pdf)

# Residual networks
  It can be generalised that increasing the depth should increase the accuracy of 
the network. But the imminent problem with increased depth is that the signal 
required to change the weights, through back propagation becomes very small at earlier 
layers. This is called vanishing gradient. 

  The second problem with training deeper networks is performing the optimization on huge parameter space and therefore 
naively adding the layers leading to higher training error. This is called degradation
problem.

  Residual networks allow training of such deep networks by constructing the network
through modules called residual models 

![" Residual Network module "](https://github.com/sbperceptron/neuralnet-notes/blob/master/residual%20learning.png)

  It can be defined as a shortcut or a skip connection from the earlier layers to 
 layers much deeper in the network. The skip connection can be used to pass the 
 activation signal to the nth layer from n-k th layer( k is the number of layers skipped). 
 The activation signal is added to the nth layer before performig the activation
 
  By this inclusion we are able to reduce the error value with increased number of 
 layers in a deep network
 
  The residual net similar to the Google net uses global average pooling followed 
 by the classification layer. The architecture is similar to the VGGNet consisting 
 mostly of 3X3 filters except we have the additional shortcut connections between
 the networks.
 !["Res Net  Example"](https://github.com/sbperceptron/neuralnet-notes/blob/master/resnet_example.png)
 
A supervised deep learning algorithm will generally achieve acceptable performance with around 5000 labeled examples per 
category and will match or exceed human level performance when trained on a dataset containing at least 10 million data examples.

though the current networks seem large from computational point of view, in fact are quite smaller than most of the primitive life forms like frogs.

RNNs such as LSTM sequence model used to model relationship between sequences and other sequences rather than fixed inputs.

Reinforcement learning for making autonomous systems learn to perform tasks by trial and error
