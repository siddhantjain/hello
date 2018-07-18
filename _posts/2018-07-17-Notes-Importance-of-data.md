---
title: Notes: Importance of data in vision
date: 2018-07-17 10:32
author: siddhantj
comments: true
category: Computer Vision
---

Some notes after going through a few papers and 16-824 lecture slides on the different aspects of data in computer vision.

1. First off I think it is important to answer as to why do we need a learning based approach for computer vision. A number of physical theories and phenomenon can be neatly explained via mathematical equations which hold true for a large number of observable cases (if not always). However, there are still many things which can not be explained via simple equations (think of almost any economic phenomena. Sure you can model it with some math, but the deviation from that model is going to be high). In such cases, where the underlying model which explains the phenomenon might be too complex, but it is easy to make a lot of observations of that model in action, we can take an example based approach. I feel like in some sense that's how humans learn a lot of complex things as well, i.e. by practice (for example no matter how hard you try to explain a beginner how to ride a bicyle, theoretically, they wouldn't be able to ride it in their first go). Further through experiments with textual data (initially and later on with visual data as well), researchers observed that a simple algorithm with more data performs better than a complicated algorithm with less data in a number of difficult problems. (Look at Unreasonable Effectiveness of Data)[https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/35179.pdf] for more on this.

2. If we look at the history of datasets in computer vision, they have increased in scale with time. Starting from barely being able to digitise an image to having datasets with number of images in the order of 10^6. Each subsequent dataset trid to undo the problems in the preceding dataset. However, since this creation of datasets has been going on for decades now, we can also accept the trend that all the datasets we have even now have some or the other problem. In (Unbiased Look at Dataset Bias)[https://ieeexplore.ieee.org/document/5995347/] they attempt to give names to these defects (termed as biases) in the datasets. In general what we want out of a lot of generic datasets in computer vision is to represent the world as we observe it. So while we are taking a sample of the world, we want to this sample to be a good representation and to test it we want algorithms that learn from this data to do well on random samples from the world as well. Hence, generalisation on different datasets should be given a lot of importance in the work done via learning. <br>
The problems that might arise in most datasets are a) selection bias (where the images are taken), b) capture bias (how are the images taken, with centering for example)  , c) categoy bias (how are the labels given) and d) negative set bias (how is representative are the rest of the images for the negative set for a given category).





















