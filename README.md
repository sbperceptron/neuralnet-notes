# Neuralnet-notes
notes on neuralnetworks

# Alexnet
1. 5 conv layers (filtersizes 11,5,3,3,3)
2. 3 fully conected layers
3. relu activations
4. dropout layer after fully conected layer

  # dropout layers 
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

# Googlenet/inception:
Best performance on image net, but deployement onto most modern gpu is a problem 
because of huge computational requirements, both in terms of memory and time. 
it is inefficient due to large width of convolutional layers. In vgg cinv operation 
every output channel is connected to every input channel and so it is called dense 
connection architecture.

" Most of the activations in a deep network are either unnecessaary ot redundant
because of correlations between them."

Therefore the most efficient architecture of a deep network will have a sparse 
connection between the activations, which impies that all output channels will
not have a cinnection with all input channels. there are techniques to prune 
out such connections which would result in asparse weight connection. But kernels 
for sparse matrix multiplication are not optimized in cuda for GPU.

so google net devised a module called inception module that approximates a sparse 
CNN with a normal dense construction. Also, it uses convolutions of different sizes 
to capture details at varied scales 

Another salient point about the module is that it has a so called bottleneck layer 
. It helps in the massive reduction of the computation requirement.

Another change that Google net made, was to replace fc layers at the wnd with a 
simple global average pooling after the last convloutional layer. This drastically
reduces the total number of parameters without reducing the accuracy.

!["inception module"](https://github.com/sbperceptron/neuralnet-notes/blob/master/inception_module.png)

# Residual networks
It can be generalised that increasing the depth should increase the accuracy of 
the network. But the imminent problem with increased depth is that the signal 
required to change the weights, through back propagation becomes very small at earlier 
layers. This is called vanishing gradient. the second problem with training deeper
networks is performing the optimization on huge parameter space and therefore 
naively adding the layers leading to higher training error. This is called degradation
problem.

Residual networks allow training of such deep networks by constructing the network
through modules called residual models 

