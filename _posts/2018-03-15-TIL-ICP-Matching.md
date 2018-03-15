---
title: TIL - ICP Matching
date: 2018-02-24 20:29
author: siddhantj
comments: true
category: SLAM
---

For some class reading and a project I am pursuing, I decided to understand the iterative closed point matching algorithm. Here is a gist of my understanding.

# What's the problem this algorithm solves?
The problem is typically with registration of point clouds. Given two point clouds, where you assume there is a lot of correspondences which are common, how do you estimate the small transformation between the two point clouds? So for example, you have point cloud reconstruction done by a quadcopter's sensing at two subsequent time steps. There might be a slight transformation between the two point clouds and the task is to estimate this transformation.


# How does ICP work?
Once the problem is understood, the approach taken by this algorithm seems pretty straightforward. It is an EM style algorithm, which eventually converges to a solution starting from some approximation of the answer. So, here is a step by step explanation of what is to be done:

Step 1: Find correspondences between points in Point Cloud 1 and Point Cloud 2
Step 2: Find a rotation matrix and translation matrix, such that when this rigid body transformaton is applied to each point in Point Cloud 1, the sum of the distances of the points from their corresponding points is minimized
Step 3: Apply the transformation to point cloud 1
Step 4: Check the sum of distances of correspondences from PC1 to PC2. Is this sum lesser than a threshold? Yes? Stop. No? No problem, go to step 1.



# Anything else?

This was a quick and dirty overview. I found the following resources useful:

1. https://www.coursera.org/learn/robotics-learning/lecture/1jDix/iterative-closest-point
2. https://www.ncbi.nlm.nih.gov/pubmed/28800096













