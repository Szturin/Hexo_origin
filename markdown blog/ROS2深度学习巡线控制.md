---
title: ROS2小车--深度学习巡线控制(1)
top: false
cover: false
toc: true
mathjax: false
date: 2023-10-21 12:42:33
author: turinJMU
img:
coverImg:
password:
summary:
---
# racing_line_follower
##### 为实现上述功能，需要视觉输入、环境感知、运动控制三大模块，其中：
- 视觉输入模块负责获取真实世界(或仿真世界)的图像并传递给下一级环境感知模块；

- 环境感知模块负责感知赛车在赛道中的位置，并将相关信息传递给运动控制模块；

- 运动控制模块根据环境感知模块输出的赛车位置信息计算得出合理的运动控制指令并下发给赛车进行对应运动。

## 视觉输入（MIPI相机驱动）
    source /opt/tros/setup.bash'
    ros2 launch mipi_cam mipi_cam_640x480_nv12_hbmem.launch.py

## 环境感知（赛道检测）
    source /opt/tros/setup.bash
    ros2 launch racing_track_detection_resnet  racing_track_detection_resnet.launch.py

## 运动控制（赛道巡线）
    source /opt/tros/local_setup.bash
    ros2 launch racing_control racing_control.launch.py

## 启动底盘
``source /opt/tros/setup.bash
ros2 launch originbot_base robot.launch.py``


## 启动相机
    # 配置 tros.b 环境：
    source /opt/tros/setup.bash
    # launch 方式启动
    ros2 launch mipi_cam mipi_cam.launch.py

mipi_cam.launch.py配置默认输出960*544分辨率NV12图像，发布的话题名称为/hbmem_img

如需使用其他分比率或者图像格式可以使用对应的launch文件，比如：

- mipi_cam_640x480_bgr8.launch.py 提供640*480分辨率，BGR8格式的图像数据
- mipi_cam_640x480_bgr8_hbmem.launch.py 提供640*480分辨率，BGR8格式的零拷贝传输图像数据
- mipi_cam_640x480_nv12_hbmem.launch.py 提供640*480分辨率，NV12格式的零拷贝传输图像数据

## 图像可视化
*使用ROS rqt_image_view*

这里采用rqt_image_view方式实现图像可视化，需要在PC端安装ROS2 Humble版本。由于发布的是原始数据，需要编码JPEG图像提高传输效率，另起一个终端用于订阅 MIPI 数据并编码为JPEG。

    source /opt/tros/setup.bash
    ros2 launch hobot_codec hobot_codec_encode.launch.py codec_out_format:=jpeg-compressed codec_pub_topic:=/image_raw/compressed
保证PC与RDK X3处于同一网段，以Foxy版本为例在PC上执行

    # 配置ROS2环境
    source /opt/ros/foxy/local_setup.bash
    ros2 run rqt_image_view rqt_image_view