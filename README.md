# zedm_capture
This is a stereo camera ROS node for the [ZED-M camera][https://www.stereolabs.com/zed-mini/], based on OpenCV VideoCapture API. The ROS node publishes left and right raw images and their camera_info.

This ROS node is mainly based on the work of Texas Instruments, with their sensor drivers in their [https://software-dl.ti.com/jacinto7/esd/robotics-sdk/08_01_00/docs/source/README.html#overview][Robotics SDK]. The are three main differences:

* The TI Robotics SDK is Docker based, while this repository runs locally
* The TI sensor drivers combine the code for ROS1 and ROS2, what can give some conflicts when build at the same time. This repository gives instructions how to build the ROS1-noetic branch.
* Each StereoLab ZED camera comes with a calibration file. The TI zed_capture software reads this calibartion file, for instance to get the baseline of the stereo camera. The ZED-M uses a different model for its disparity model. This repository contains a script that can also read the calibration files of a ZED-M camera
