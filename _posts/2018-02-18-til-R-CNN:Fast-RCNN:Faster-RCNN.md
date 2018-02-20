---
title: TIL - R-CNN/Fast RCNN/Faster RCNN
date: 2018-02-18 12:48
author: siddhantj
comments: true
category: Computer Vision
---

Writing this post as a way to archive my notes while reading the series of papers: R-CNN, Fast R-CNN and Faster R-CNN. The last in the series is our first reading for the course 16-824: Visual Learning And Recognition at CMU. My hope is that the semester allows me enough time to write these notes for each of the readings. So far, so good, I guess.

So, what problem are we trying to solve here? The broad problem is object detection and segmentation. Basically, given an image, being able to segment out objects from that image. That is for each pixel in the image, giving a label corresponding to the object it belong to (it is possible that some pixels belong to no object).

The focus in this post is on Faster R-CNN, so I will quickly go over the first two, R-CNN and fast R-CNN and try to cover Faster R-CNN in full depth.

# [R-CNN](https://arxiv.org/abs/1311.2524)

In this paper, the authors feel they had two major contributions/discovers.

a) CNNs can be used for object detection/segmentation as well by applying them to "region proposals" (more on that later).
b) In case of low data samples, training with an existing large dataset and subsequently fine tuning it can actually give reasonably good results.

From a bird's eye view, the way this system works is as follows:

1. Get a lot of region proposals in the given image. Region proposals are parts of the image which may have an object in it. How do you find region proposals? Read on.
2. Then you convert these region proposals into a form that AlexNet understands (i.e. 227x227 images)
3. Then you find the FC8 features from AlexNet for these region proposals
4. Finally, you run these features through 'n' SVM classifiers, each corresponding to one of the objects in the system. Thus for each class, you have a score for each of the region proposals. You reject regions which have an IOU (area of overlap / area of union) greater than a threshold with another region. Now it is a little unclear to me how are they deciding the final region proposal. But here is what I have concluded for now: For each region, find the class for which it has the highest score. For each of the region it intersects with, check if the two regions have the same classes. If they do, only keep the ones with the higher score.

## How do you find region proposals?
They use something called selective search. There are many more methods and in the interest of time, I didn't look at all of them right now. What I have read elsewhere is that the way selective search works is to look at an image through windows of various sizes and then proposing regions if that particular window makes sense as a region based on the similarity of pixels and some other features in the region. I should come back to this section and update it once I understand how it works.

So here is how it works:
First segment the image using a similarity measures like color (this method is graph based). Next, start grouping adjacent segments based on similarity. Similarity is calculated as a score of colour, texture, shape and size. once we have no more segments to group, we return the bounding boxes for the segment.

## Some notes on the training/testing of the system
While training, the authors first train ImageNet on AlexNet. They then do away with the last layer of 1000 classes and instead introduce a new 21 class layer (each corresponding to one of the objects). After this, they run the different regions (which have an IOU greater than a threshold with a ground truth box) through this network. we also have 21 linear SVMs trained for each of the classes, that are used for final object labels.


## Extension to Segmentation
Note that so far, we have only done Object Detection, but not object segmentation. How do we go from these bounding boxes to pixel level labels? This is also an eventual TODO, to understand how to go from region classification to semantic segmentation.


# [Fast R-CNN](https://arxiv.org/abs/1504.08083)

This method is an attempt to improve on the speed of R-CNN. In R-CNN we saw that the approach was to find region proposals and then run each region proposal through a CNN, to get some classification scores. Now, we are clearly doing some redundant calculation here because many of these region proposals overlap with each other. So, in this paper, the broad idea is to first run the entire image through the CNN and get a convolution map for it. So, imagine, we have a image of dimensions I~H X I~W. Because of pooling layers, we will be bringing this down to dimensions I~h X I~w. So now, we find the features corresponding to each region proposal by finding the corresponding location for a region proposal in the convolution map (take a break and think about how this can be done. Go back to how we find correspondences when doing backpropogation to find the influence of a particular weight in the derivative of the loss function). Once, this is done, the authors introduce a new layer, termed, ROI Pooling. This layers converts each ROI feature map of varying sizes into a fixed sixed feature vector. The feature vector finally feed into a set of fully connected layers that branch into two output layers, one that gives softmax probability estimates over the object classes and another that gives a refined bounding box position for this region.

Some interesting things to know:

## ROI Pooling
I am not sure if this is the first paper to use ROI Pooling, but this is the first time I came across the concept. This layer takes in a feature map of any size and converts it into a feature map of a fixed size by using max pooling. The final H and W of the output feature map are hyper parameters for the pooling layer. The way it works is that given any large feature map, first dividee the feature map in sub-grids, such that we have H X W subgrids (where H and W are the hyper parameters we discussed above). Now, do a max pool of the values in each of the sub-grids, to evaluate the feature map. The derivate calculation methodology is mentioned in the paper and probably worth a  read if you are feeling motivated.

## Multi-task loss
Another interesting concept in the paper is that of the mutitask loss. As I noted earlier, in this system, we finally branch out to two outputs, one corresponding to the softmax classification for a region and another corresponding to the bounding box estimate. The loss function in such a case is sum of individual losses for the bounding box and the classification. This can be a weighted sum, but in the paper at least the weights are equal. In the paper they have done experiments to demonstrate how having a multi-class loss improves the accuracy of the overall system (as compared to having individual losses). Interesting read, can check it out.

# [Faster R-CNN](https://arxiv.org/pdf/1506.01497.pdf)
 And now finally, the raison d'être for this entire post. It's weird how the authors incremently worked on these ideas, almost like a T.V show, where they had a plot in mind and slowly revealed each aspect of the plot through different publications (will they have the guts to claim a season finale with Fastest R-CNN?). Anywho, so far we saw that with fast R-CNN, a improvement in speed was achieved by doing away with redundant calculations while running region proposals through a CNN. However the bottleneck remained in calculating the region proposals themselves. So, now the contribution/innovation is in doing away with the classical region proposal techniques and use a learning based system for the region proposals as well.

Here is a quick summary:

In the R-CNN/Fast R-CNN paper, finding region proposals is done in an unsupervised manner. They look at properties (such as colour, texture, shape etc.) in the image to find bounding boxes around parts of the region where there is a chance of an object.
However, the authors note that finding these region proposals is expensive. They observe that the object detection phase is already calculating interesting features (in a hierarchical manner) in an image. Some of these calculations should be useful in finding out regions of interests in the image as well. Hence, they club the two together in one system.

So, they start with running a given image through a CNN to obtain a convolution map of the image. This convolutional map feeds into a Region Proposal Network - a Fully Convolutional Network that provides region proposals. The region proposals along with the feature map that was used to calculate these region proposals go into the object detection system (Fast R-CNN). Thus, finally, obtaining labelled bounding boxes in the image.






