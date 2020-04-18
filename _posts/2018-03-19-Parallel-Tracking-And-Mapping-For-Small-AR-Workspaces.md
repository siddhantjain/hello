---
title: Parallel tracking and mappping for small AR workspaces
date: 2018-03-19 20:29
author: siddhantj
comments: true
category: SLAM
---

This is a summary of a paper i recently read. The paper can be found here: [http://www.robots.ox.ac.uk/~gk/publications/KleinMurray2007ISMAR.pdf](http://www.robots.ox.ac.uk/~gk/publications/KleinMurray2007ISMAR.pdf)

# What is the problem that is being addressed?
We want to estimate the pose (x,y,z, theta) of a camera in a scene the camera has not scene previously. This paper was released in 2007 and considered to be an important work on the field. Hopefully through this summary, i will be able to summarise the important ideas in the paper.


# What do the previous approaches look like?
If the map of the scene is known, previous approaches will use this map to estimate the pose of the camera. Basically, these approaches will look for features in the scene. It will then compare these features with the known map and use this comparison to estimate the warp in the features. The warp in the features can be applied to the warp in the stored pose estimates of the camera when the map was created. However, of course, we may not know a lot of features in advance, so some "extensible mapping" techniques will require the camera to initialise with just one known feature. They will then keep building the map from here as and when they observe new features.



# What's the brave new idea in this paper?

This paper targets to do the estimation of the camera pose without any prior information whatsoever. This is the same goal as being able to create a map of the an "unknown scene without any known objects or initialisation target" and also knowing where in this map does the camera lie, simultaneously. Wait a minute, isn't this the exact SLAM problem statement? Exactly. Good question. in this paper, they are avoiding doing SLAM because they feel the approaches that existed at that time were not as robust. Instead, they dropped the simultaneous and instead made it Parallel Localisation and Mapping.

# So, how is all of this done?
As noted already, in the work, mapping and tracking are done parallely in an attempting to cut down on the speed and accuracy hit if these two tasks are coupled. So let's first understand how is the map represented in the first place.

## Map representation
The map is represented through some point features located in the world coordinate frame. The location of each point in the map is thus represented  by (x,y,z,1) in the world coordinate frame. In addition to the location, each point also has an associated patch and a normal with it. This patch is the pixels in its local, planar neighbourhood and the normal of that plane is stored.

For storing the pixels of the neighbourhood with the points features, the system actually stores a set of frames. These frames are typically frames where some point features were first observed. So the point features themselves simply store a location in the keyframe for their corresponding patch.

## Tracking
In tracking we want to find the new pose of the camera, given we know the old the pose and also the map, of course. The approach to do tracking is then as follows:


For tracking there are steps given in the paper which are probably the best description, but I will try to rephrase to test  my understanding:

1. Since you know the pose of the camera in the previous frame, you use some kind of a motion model (simply by seeing the difference in the poses of the last two camera poses) to estimate the pose in the next frame.
2. Project all the map points you have right now into the image
3. Search of a small, fixed number of features
4. If you find some matches, update the pose
5. Search for a larger number of features now
6. If you find matches, update the pose

each of these steps are described in more detail in the paper and I am taking the easy way out now by stopping here and referring to the paper instead.

Also check out the robust optimisation technique used in the paper.

## Mapping

The mapping system employs a user assisted initialisation system where the user takes a picture and then moves the camera smoothly by small translation and takes another picture. These two pictures are used along with the 5-point algorithm ( I need to read what this algorithm is and update this link) to get an initial estimate of the map. This estimate is then used in the tracking system as well. After this initial estimate, for each key frame we check if it is previously unseen keyframe. If it is unseen, we might add it to the the set of keyframes if it is sufficienly away from the last added frame and also the camera position should be sufficiently away from the closest key point which is there in the map and in the keyframe being considered. Whenever a keyframe is added, a bundle adjustment is done for all keyframes and the points in the map. This helps in keeping the system from not accumulating errors over time.

Currently my understanding of the mapping system is a little lacking, but this will be discussed further in the class and I might add more notes after the class. If not, I really liked the paper  as it was more self contained than most other papers I read and hence not as bad a read - so maybe, I can check it out another time and update this section!

Note that the map is scaled to metric units and the dominant plane is made to lie at z=0

















