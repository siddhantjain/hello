---
title: Simultaneous Localisation and Mapping for Landing Site evaluation for drones
desc: A complete SLAM system to evaluate the ground plane for potential landing sites
proj-url: (https://siddhantjain.github.io/files/landing-site-slam.pdf)

---
This project was done as a part of coursework for 16-833 (Robot Localisation and Mapping) at Carnegie Mellon University

A drone trying to land autonomously needs the ability to evaluate various parts of the ground underneath for their suitability as a landing site. In this work, we developed one pipeline that can perform this evaluation real-time by fusing together a semi-direct visual odometry along with a non-linear ICP. We eventually generate the map as a point cloud, which is then fed into another module for evaluation based on the slope and roughness of the generated point cloud. 

## System Overview
The following diagram gives an overview of the system we developed along with highlighting the core components used:

<img src="siddhantjain.github.io/images/system_overview.png"
alt="System Overview"
style="float: left; margin-right: 10px;" />


here is a link to a presentation for this work:

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQR2uSJ4D_u4DPDmUxQLdHcBKs3npcm6p5xmnL7RezcFAe3CMYzk_cyg6P9DsTtQsHZ5lGwFqdyyINQ/embed?start=false&loop=false&delayms=10000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


For more details, check out our write-up for this work here: https://siddhantjain.github.io/files/landing-site-slam.pdf
