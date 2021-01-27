# darknet-ROS integration for use in gazebo

## Overview
This is a [forked repository](https://github.com/leggedrobotics/darknet_ros). This repo was used to perform object detection on the gazebo implementation of SAUVC'20 pool. A custom object detector was trained using YOLOv3 on darknet. Its corresponding weights and cfg file can be found in this repository.

## Download this repository
```cd catkin_workspace/src
git clone --recursive https://github.com/SubZer0811/darknet_ros
cd ../
```

## Build
Using [Catkin Command Line Tools](http://catkin-tools.readthedocs.io/en/latest/index.html#):
```
catkin build darknet_ros -DCMAKE_BUILD_TYPE=Release
```

## Setup
- **camera_topic**: change the topic at `darknet_ros/config/ros.yaml` (line 4)
- **weight_path** and **cfg_path**: `darknet_ros/config/yolov3_auv_sim_gate_obstacle_v1.yaml` is the file that contains the paths to cfg and weights file for darknet to use. weights and .cfg files need to placed at `darknet_ros/darknet_ros/yolo_network_config/weights` and `darknet_ros/darknet_ros/yolo_network_config/cfg` respectively.
- **disabling frame output**: toggle enable_opencv under imagee_view to enable and disable displaying the inferred frame in `darknet_ros/config/ros.yaml` (line 31)
- **frame rate**: Changing the `rate` value at `ros.yaml` will change the output frame rate of darknet_ros.

## Run
```
roslaunch darknet_ros yolo_v3.launch
```

## Description

`/darknet_ros/detection_image_WL`: topic that publishes images that are inferred without labels. <br>
`/darknet_ros/detection_image`: topic that publishes images that are inferred

`seq` in `/darknet_ros/bounding_boxes` is mapped to `seq` in `/darknet_ros/detection_image_WL`.