<img src=https://cdn.stereolabs.com/assets/images/logo/logo_stereolabs.svg width=150 alt="StereoLabs">

# zedm_capture
This is an unofficial stereo camera ROS node for the [ZED-M camera](https://www.stereolabs.com/zed-mini/), based on OpenCV VideoCapture API. The ROS node publishes left and right raw images and their camera_info.

The official [zed-ros-wrapper](https://github.com/stereolabs/zed-ros-wrapper) contains much more functionality, but requires that the ZED SDK is installed. The ZED SDK requires a computer with a Nvidia GPU, which is not always available on each robot and/or laptop. This node can run on any machine.

The ZED-M is the mini-version of the range of stereo-cameras provided by [StereoLabs](https://www.stereolabs.com/). The [ZED Mini](https://www.stereolabs.com/blog/introducing-zed-mini/) features dual high-speed 2K image sensors and a 110 degree field of view. With an eye separation of 63 mm, the camera senses depth from 0.1 meters to 12 meters, which is very usefull near range in robotics. With both cameras in Ultra-Depth mode, the range of the camera can be increased to 20 meters. 

<div align=center>
<img src=https://cdn.stereolabs.com/blog/wp-content/uploads/2017/09/zed-mini.jpg width=450 alt="ZED-M"><br>
The ZED-M stereo camera. Courtesy StereoLab
</div>
<br>

This ROS node is mainly based on the work of Texas Instruments, with their sensor drivers in their [Robotics SDK][https://software-dl.ti.com/jacinto7/esd/robotics-sdk/08_01_00/docs/source/README.html#overview]. There are three main differences:

* The TI Robotics SDK is Docker based, while this repository runs locally
* The TI sensor drivers combine the code for ROS1 and ROS2, what can give some conflicts when build at the same time. This repository gives instructions how to build the ROS1-noetic branch.
* Each StereoLab ZED camera comes with a calibration file. The TI zed_capture software reads this calibartion file, for instance to get the baseline of the stereo camera. The ZED-M uses a different model for its disparity model. This repository contains a script that can also read the calibration files of a ZED-M camera
