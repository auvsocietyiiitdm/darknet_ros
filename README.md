# darknet-ROS integration for use in gazebo

## Overview
This is a forked repository. This repo was used to perform object detection on the gazebo implementation of SAUVC'20 pool. A custom object detector was trained using YOLOv3 on darknet. Its corresponding weights and cfg file can be found in this repository.

## Install
Follow the steps mentioned here: https://github.com/leggedrobotics/darknet_ros <br>
Make sure that the name of the camera topic is **camera/rgb/image_raw**

## Run
```
roslaunch darknet_ros darknet_ros.launch
```
