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
- **frame rate**: Changing the `rate` (in Hz) value at `ros.yaml` will change the output frame rate of darknet_ros.

## Run
```
roslaunch darknet_ros yolo_v3.launch
```

## Actions
An image can be sent the action server `/darknet_ros/check_for_objects/`.

## Documentation

### Publishers
`/darknet_ros/detection_image_WL`: This topic publishes images that are inferred without labels. <br>
`/darknet_ros/detection_image`: This topic publishes images that are inferred by the neural network.
`/darknet_ros/bounding_boxes`: This topic publishes the detected objects with bounding boxes in yolo format.
`/darknet_ros/found_object`: This topic publishes the sequence number, frame id and number of detected objects in the same frame.

### Subscribers
`/auv_v2/f_cam/image_raw`: This is the topic that darknet_ros subscribes to recieve frames from the camera.

The queue size of every topic has been set to 1 to achieve a real time feedback.

### config files
There are 2 configuration files (excluding the cfg file required by **darknet**) that are essential to run darknet_ros.
- `darknet_ros/config/ros.yaml`: This file contains the details of the various subscribers and publishers used. Setting the frame rate and frame output is done at this file.
- `darknet_ros/config/<darknet_config_file>.yaml`: This file holds the path to weights and cfg files required by darknet. The threshold of detection can be set here. This file also consists of all the classes used by the neural network.

### Important points to keep in mind
The default method is to discard boundboxes with height and width less than `0.01`. For now, this value has been set to `0.001`.