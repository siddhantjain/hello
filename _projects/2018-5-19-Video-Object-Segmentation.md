---
title: One shot learning for video object segmentation using 3D convolutions
desc: Using 3D convolutions and kinetics pre-training to perform object segmentation in videos
proj-url: (https://siddhantjain.github.io/files/video_object_segmentation_fully_convolutional_i3d.pdf)

---

In this project we explored a new direction for performing video segmentation, i.e. using the I3D network architecture with the pre-trained weights from the training of the kinetic dataset. We adapted the I3D network into a Fully Convolutional Network adding upsampling layers at various stages to give us the final segmentation map. This allowed us to look at all frames of the videos at once giving a superior method to segment the video but at the same time it also introduced some unique problems that we address in this work.

We test our algorithm on the dataset released for the DAVIS challenge where the task is to propagate the segmentation in the first frame to all subsequent frames. In order to adapt to a particular video, we devise a one-shot learning approach that fine-tunes the network based on the single annotated frame it receives. We "hallucinate" the remaining frames of the video with annotations via geometric perturbations. Once we have a reasonable number of frames, we do one step of fine tuning on the network by using these hallucinated frames as ground truth. Finally, owing to its large size, fitting full resolution videos for the I3D network on the GPU is a challenge. We tackle this problem by fusing results from overlapped crops of the full res video. 


For more details, check out our write-up for this work here: [Link to Write-up](https://siddhantjain.github.io/files/video_object_segmentation_fully_convolutional_i3d.pdf)
