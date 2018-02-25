---
title: TIL - Bayes Filters
date: 2018-02-24 20:29
author: siddhantj
comments: true
category: SLAM
---

I am doing a course in Robot Localisation and Mapping this semester which shall hopefully trigger a bunch of posts where I try to explain concepts in the course to myself. Here is the first in that series, Bayes Filter: the foundational algorithm for state estimation.


# Some context
We have a robot in some environment. This robot might have position (termed as pose) and the environment might have some configuation as well. This combination of the robot position plus the environment configuration is termed as a **state**. Now, the robot can perform some action, which may or may not change the state. The idea of robot performing an action is called a **control**. Finally, the robot can try to sense it's environment and make some observations (take an image, report a lidar reading etc.) which is called a **measurement**.

Bayes filter (and consecutively many more things in SLAM in general) are an interplay of these states, measurements and controls. We assume that nothing is certain and hence completely work with probability distrubutions to make inferences. Our goal is to have some **belief** about the **state** of the robot given the measurements the robot is making.


# So, what is a Bayes Filter?
From what I understood so far, Bayes Filter is an algorithm/framework that let's you calculate ( and progressively refine ) an estimate of the the state of a robot (plus environment) using the various controls that robot is executing and the measurements that the robot is noting. Just to fuel the imagination, controls can mean moving around, opening a door, picking an object etc. Similarly measurements can mean the odometry reading, pictures, lidar scans etc.

Let the random variable x represent the state of the system. This means, x is a probability distribution function that gives the probability associate with each possible state. Now, what we do in bayes filter is to start with some initialisation for x (generally a uniform probability distribution) and then we update x to incorporate our controls and measurements. states are defined at different discreet units of time. So we start with x<sub>0</sub> and successively calculate x<sub>1</sub>, x<sub>2</sub> etc.



# Understanding the algorithm

Formally the algorithm is as follows


Algorithm Bayes_filter(bel(x<sub>t−1</sub>), u<sub>t</sub>, z<sub>t</sub>):
1. for all xt do
2.   bel_hat(x<sub>t</sub>) = Integral(p(x<sub>t</sub> | u<sub>t</sub>, x<sub>t−1</sub>) bel(x<sub>t−1</sub>) dx<sub>t−1</sub>)
3.  bel(x<sub>t</sub>) = η p(z<sub>t</sub> | x<sub>t</sub>) bel_hat(x<sub>t</sub>)
4. endfor
5. return bel(x<sub>t</sub>)

So bel_hat is what we call the prediction. If we know the previous state and the control execute in this state, we can have a prediction for our current state. If you look at step 2, all we are doing is calculating is the expected value of the probability of each state. Whereas step 3 is an application of bayes rule, which incorporates our mearument in our calculation of belief.

Look at step 2 again. We are taking each possible state at time t-1 and multiplying the probability associated with being in that state with the probability that control u<sub>t</sub> lead to a state transition from x<sub>t-1</sub> to x<sub>t</sub>

In step 3, we are calculating the probability of a particular state (x<sub> t </sub>) given the measurement ( z <sub> t </sub>) by using bayes rules.


# I am still a little hazy, how should I solidify what I understood

Nothing is better than an example. head over to section 2.4.2 in Probabilitic Robotics by Thrun et. al.












