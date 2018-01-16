---
title: Segmentation Based Data Augmentation
desc: Improving classifier accuracy by a novel data augmentation method
proj-url: https://github.com/siddhantjain/SegDataAugmentation

---
This project was done as a part of coursework for 16-720B (Introduction to Computer Vision) at Carnegie Mellon University

In this project, we propose a new method to do data augmentation for object detection tasks. Instead of using basic manipulations like rotation, color jitter etc, we experimented with going up by one level of abstraction. We model our images as a combination of foreground, i.e the object to be detected and background - a valid setting in which the object can be found. A class of n data points, has thus ‘N’ valid models in which the object is found in the world and also N valid settings in which the object is found. We augment the data by generating N^2 - N new datapoints for a class by blending the each foreground with the remaining backgrounds found in the class.

For our experiments we used the Caltech101 dataset and fine tuned a pre-trained network to do the classification task. We felt the following questions were important to answer to test our method:

* Does it reduce overfitting?
 We observed that this method does help in reducing overfitting by noticing a reduction in the test error rates

* How well does it work with other forms of data augmentation?
We saw that this method can work in conjunction with other methods. We augmented the image with rotations and observed that it doesn’t tank the classifier performance. Instead, it actually improves it a little.

** Future Work

* We want to test this method on other datasets and also see if we can combine different datasets
* Can we use a generator/discriminator based system to generate backgrounds for replacement
* How do we generate image blends which look more like natural images

here is a link to a presentation for this work:

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSBXNjYhFFFedc2l75zAXxk1WEMvfLC7HAvBY9gt8gnsxJb9mpBZEBWqCWJ39t1BxOt53hw-m_Ce6W7/embed?start=false&loop=false&delayms=5000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


Project code can be found here: https://github.com/siddhantjain/SegDataAugmentation
