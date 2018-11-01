---
layout: post
title: Image Super Resolution using Deep Convolutional Networks
---

#### Overview

Recovering a high-resolution image from a single low-resolution image – Single Image Super-Resolution – is one of the classical problems
in computer vision. The single-image super resolution algorithms can be categorized into four types – examples-based methods, predictions
models, edge based methods and image statistical methods. Among them, the example-based methods achieve the state-of-the-art performance.

One of the example-based super-resolution methods is sparse-coding based method. It performs the following steps for image super-resolution 
in its solution pipeline.

1.	First it crops overlapping patches from the input image and pre-process it (e.g. subtracting mean and normalization). 
2.	These patches are then encoded by a low-resolution dictionary. 
3.	These sparse coefficients are then passed into a high-resolution dictionary for reconstructing high-resolution patches. 
4.	The overlapping reconstructed patches are aggregated (e.g. by weighted averaging) to produce the final output. 

This paper shows that the aforementioned pipeline is equivalent to a deep convolutional neural network. The proposed name of the model is 
Super-Resolution Convolutional Neural Network (SRCNN). Overall, the contributions of this study are mainly in three aspects:

1.	A fully convolutional neural network for image super-resolution is presented. The network directly learns an end-to-end mapping between
the low- and high-resolution images, with little pre/post processing beyond the optimization.
2.	A relationship between deep learning-based SR method and the traditional sparse-coding-based SR methods is established. 
This relationship provides a guidance for the design of the network structure.
3.	Deep learning is useful in the classical computer vision problem of super-resolution, and can achieve good quality and speed.

#### SRCNN

There are three operations to be performed for the method to work: Patch extraction and representation, Non-linear mapping and 
Reconstruction.

Patch Extraction and Representation: This operation extracts overlapping patches from the low-resolution image and represents each patch 
as a high-dimensional vector. These vectors comprise a set of feature maps, and the number of feature maps equals to the dimensionality 
of the vectors.

Non-linear mapping: This operation nonlinearly maps each high-dimensional vector onto another high-dimensional vector. Each mapped vector 
is conceptually the representation of a high-resolution patch. These vectors comprise another set of feature maps.

Reconstruction: This operation aggregates the above high-resolution patch-wise representations to generate the final high-resolution image. 
This image is expected to be similar to the original image.

These steps are depicted in the following picture:

![alt text](https://hassanms.com/images/sr.png "SRCNN")

#### Experiments

The authors first investigate the impact of using different datasets on the model performance. Then they explore different architecture 
designs of the network, and study the relations between super-resolution performance and factors like depth, number of filters, and 
filter sizes. Subsequently, the proposed method is compared with the state-of-the-arts both quantitatively and qualitatively. 

For comparison, they use a relatively small training set that consists of 91 images, and a large training set that consists of 395,909 
images from the ILSVRC 2013 ImageNet detection training partition. The training time on ImageNet is about the same as on the 91-image 
dataset since the number of backpropagations is the same. The SRCNN achieves 32.52 dB, higher than 32.39 dB yielded by that trained 
on 91 images. The results positively indicate that SRCNN performance may be further booster using a larger training set, but the 
effect of big data is not as impressive as that shown in high-level vision problems.

In general, the performance would improve if we increase the network width, i.e. adding more filters, at the cost of running time. 
However, if a fast restoration speed is desired, a small network width is preferred, which could still achieve better performance 
than the sparse-coding-based method (31.42 dB).

Recent studies suggest that CNN could benefit from increasing the depth of network moderately. Authors conduct controlled experiments
which add additional layers to the original network. All these experiments indicate that it is not “the deeper the better” in this 
deep model for super-resolution.
