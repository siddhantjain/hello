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





