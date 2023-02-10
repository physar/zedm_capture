<img src=https://cdn.stereolabs.com/assets/images/logo/logo_stereolabs.svg width=150 alt="StereoLabs">

# zedm_capture
This is an unofficial stereo camera ROS node for the [ZED-M camera](https://www.stereolabs.com/zed-mini/), based on OpenCV VideoCapture API. The ROS node publishes left and right raw images and their camera_info.

The official [zed-ros-wrapper](https://github.com/stereolabs/zed-ros-wrapper) contains much more functionality, but requires that the [ZED SDK](https://www.stereolabs.com/developers/) is installed. The ZED SDK requires a computer with a [Nvidia GPU](https://www.stereolabs.com/developers/nvidia/), which is not always available on each robot and/or laptop. This node can run on any machine.

The ZED-M is the mini-version of the range of stereo-cameras provided by [StereoLabs](https://www.stereolabs.com/). The [ZED Mini](https://www.stereolabs.com/blog/introducing-zed-mini/) features dual high-speed 2K image sensors and a 110 degree field of view. With an eye separation of 63 mm, the camera senses depth from 0.1 meters to 12 meters, which is very usefull near range in robotics. With both cameras in Ultra-Depth mode, the range of the camera can be increased to 20 meters. 

<div align=center>
<img src=https://cdn.stereolabs.com/blog/wp-content/uploads/2017/09/zed-mini.jpg width=450 alt="ZED-M"><br>
The ZED-M stereo camera. Courtesy StereoLab
</div>
<br>

This ROS node is mainly based on the work of Texas Instruments, with their sensor drivers in their [Robotics SDK](https://software-dl.ti.com/jacinto7/esd/robotics-sdk/08_01_00/docs/source/README.html#overview). There are three main differences:

* The TI Robotics SDK is Docker based, while this repository runs locally
* The TI sensor drivers combine the code for ROS1 and ROS2, what can give some conflicts when build at the same time. This repository gives instructions how to build the ROS1-noetic branch.
* Each StereoLab ZED camera comes with a calibration file. The TI zed_capture software reads this calibartion file, for instance to get the baseline of the stereo camera. The ZED-M uses a different model for its disparity model. This repository contains a script that can also read the calibration files of a ZED-M camera

### Known issues

* The description does not contain all coordinate frame transitions needed by RVIZ (yet)
* The software is currently tested on one computer (ros-noetic), more tests are on the way.

## Installation

### Prerequisites

* [Ubuntu 20:04 ( Focal Fossa)](http://releases.ubuntu.com/focal/)

* [ROS1 Noetic Ninjemys](http://wiki.ros.org/noetic/Installation/Ubuntu)

If the ros-noetic is not already in your package list, add it

```bash
sudo apt update && sudo apt install curl gnupg2 lsb-release
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros-latest.list > /dev/null

sudo apt update
```

This ros-node is using the following ros-packages:


```bash
sudo apt install ros-noetic-ros-base
sudo apt install ros-noetic-rviz
sudo apt install ros-noetic-xacro
```

###  TI Robotics SDK

The latest version of the sensor drivers in the Texas Instruments [Robotics SDK](https://software-dl.ti.com/jacinto7/esd/robotics-sdk/08_01_00/docs/source/README.html#overview) can be build from source by the following commands:

```bash
mkdir ~/git
cd ~/git
git clone git://git.ti.com/processor-sdk-vision/jacinto_ros_perception.git
```

The directory contains some tools and the code for both ROS1 and ROS2. To build the ROS1 driver, you could execture the commands:

``bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
ln -s ~/git/jacinto_ros1_perception/ros1 jacinto_ros1_perception
ln -s ~/git/jacinto_ros1_perception/cmake .
ln -s ~/git/jacinto_ros1_perception/tools .




