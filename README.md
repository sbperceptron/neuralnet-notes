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
at a lower cost
!["VGG16 Architecture"](https://github.com/sbperceptron/neuralnet-notes/blob/master/VGGNet.png)

