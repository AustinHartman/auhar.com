---
title: "Some notes on a CNN for DNA"
layout: post
---

The goal of this post is to train a CNN to learn the difference between short pieces of DNA from humans and mice.

In order to decide if a piece of DNA is from a mouse or a human, I used a simple network with a single convolutional layer. It’s followed by a couple of dropout and fully-connected layers ultimately leading to a prediction between 0 and 1. A score close to 1 indicates the piece of DNA is probably from the human genome and close to zero indicates the DNA is probably from the mouse genome. In order to allow a DNA sequence to be inperpretted by the network, I one-hot encoded each sequence before passing it to the input layer.

I trained the model on 30,000 fragments evenly split between the mouse and human genomes from chromosomes 1, 10, and 11. Once I was all done training, I tested performance on 10,000 sequences from chromosome 17 of the mouse and human genome.

![stock](/assets/architecture.png)

### Does it work?
I was a bit surprised to see that such a simple model really had any predictive ability at all. Since the GC content of the mouse and human genome is quite similar (42% vs 41%), the network can’t simply make predictions based on the abundance of different nucleotides. Further, the network is so shallow compared to what is commonly used, I figured it would require training with a lot more data on a much larger architecture to make decent predictions. The network includes a single convolutional layer followed by two fully connected layers which intuitively means the model is only able to learn short motifs that in combination with other motifs predict the origin of the DNA sequence. The filters in the convolutional layer learn to detect predictive motifs, while the fully connected filters learn useful combinations of motifs. Although the performance of the model isn’t great compared to what we’ve seen from other CNNs, it’s kind of nice on an intuitive level that such a shallow network actually has some predictive ability.

![stock](/assets/cnn_loss.png)
![stock](/assets/cnn_accuracy.png)
![stock](/assets/cnn_roc.png)

### More on training
My first attempt at building a network didn't include any dropout layers, but they proved to be crucial for preventing overfitting. Without them, the model loss continually decreased during each epoch for the training data, while the test data’s loss would quickly flatline. During training I tried twisting a bunch of different knobs; I modified the training rate, momentum, where I placed the dropout layer(s), and the length of the input fragments. I picked training parameters that converged quickly, but without lowering the accuracy, and I noticed that using longer DNA sequences led to higher accuracy, which makes sense.

### Limitations
This sort of classification problem probably isn't useful, but I think the act of translating a classification problem into a network to answer it was useful. But still, it would be more useful to classify other things like whether or not some transcription factor will bind to a bit of DNA, or whether chromatin is open or closed. Maybe I’ll look at that another time. Another big weakness of this network is the architecture itself. A state of the art network would use far more convolutional layers to learn higher level patterns. As it stands, the network is only able to learn patterns centered around short k-mers where k represents the width of the convolutional filters used. Further, out of the box CNNs are not designed to model DNA strands. This is problematic because the reverse complement of any input sequence should have the same output. Often this is the case, but there is nothing constraining the network from diverging so on occasion it will.

Here’s the code used to build it: [CNN gist][network-code]

[network-code]: https://gist.github.com/AustinHartman/9cd9341ab716bb6316d413d0028226a8
