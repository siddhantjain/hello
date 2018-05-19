---
title: TIL - Deconvolution
date: 2018-04-23 10:32
author: siddhantj
comments: true
category: Computer Vision
---

While, I had a hand-wavy idea about deconvolution earlier, for a project I had to properly understand the concept. Hence, taking a few minutes off to write a quick note about deconvolution layers

# Context:
In CNNs we generally have the input downscaled to a smaller size because of the max-pooling and all. This all nice when our final output is anyway much smaller in dimensions from the input. However, when addressing problems like segmentation, we want the the output size to be similar to the input size (per pixel classification). In order to do that, we can simply interpolate (resize) the output to the input size. But, that's a constant interpolation which is not tuned to the data we have. Hence, deconvolution layers that upscale inputs through a method that it learns by looking at the task at hand. 


# How do deconvolution layers work?
Exactly like convolution layers! Except, in deconvolution we insert zeros in-between the cells of the input. Also, instead of normal intialisation of the kernel, we do an initialisation such that the kernel is performing a bi-linear interpolation, when initialised. 


# Is that it? Anything else?

Yeah, that's more or less I want to say for this post. Just want to add that deconvolution is an unfortunate name that caught on (and I am guilty of perpetuating it as well). It's unfortunate because this is no different than convolution itself (and deconvolution has slightly different meaning in signal processing) . People like to call it transposed convolution.

# Any references?
Yes, two!

I mean not really references, but good resources that helped with my quick understading. Check them out.

1. (https://datascience.stackexchange.com/questions/6107/what-are-deconvolutional-layers)[https://datascience.stackexchange.com/questions/6107/what-are-deconvolutional-layers]
2. (http://cv-tricks.com/image-segmentation/transpose-convolution-in-tensorflow/)[http://cv-tricks.com/image-segmentation/transpose-convolution-in-tensorflow/]
















