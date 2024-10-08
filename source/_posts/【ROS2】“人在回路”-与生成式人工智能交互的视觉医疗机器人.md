---
title: 【ROS2】“人在回路”---与生成式人工智能交互的视觉医疗机器人
top: false
cover: /img/blog_cover/ros2.png
toc: true
mathjax: false
abbrlink: 17498
date: 2024-04-28 00:39:25
author:
img:
coverImg:
password:
  - 编程
  - ROS2
  - linux
tags:
- ROS2
- linux
- 操作系统
- RDK X3
categories:
  - - 学习笔记
    - ROS2
  - - 人工智能
    - ROS2
  - - RDK X3
  - - Linux
    - Ubuntu
---

# “人在回路”---与生成式人工智能交互的视觉服务机器人

**第一次更新：2024.4.28**

## 前言

- 人在回路（Human-in-the-loop）是一种模式，类似于人机闭环系统或人机互助系统。这种模式被认为是机器学习、人工智能和机器智能的一种可行发展模式，需要人与机器之间的相互作用。在这种模式下，人类始终是模型的一部分，影响着模型的结果，并且需要人类的智能来帮助机器更加智能化。
- ChatGPT是一款强大的基于深度学习的自然语言处理模型，能够生成高质量的自然语言文本。使用ChatGPT+TogetheROS，即ChatRobot将文字描述转化为小车控制指令，根据描述生成特定功能的代码，使机器人按照描述执行相应的任务。--转自NodeHube社区。--转自NobeHube

## 项目信息：

**我们的机器人定位为医疗看护机器人（无人车），使用RDK X3 嵌入式AI开发板作为主控，通过Opencv等进行视觉识别，基于类似激光雷达测距的方法实现自主导航运动，满足不同场景下的控制需求。通过ROS2系统使小车与计算机进行通信。**

**我们计划使用OpenAI提供的API接口写入小车系统，实现初步的语音交互到控制的过程。基于搭载ROS2系统的RDK X3开发板，使用"人在回路"的模型训练方法，完善机器人行为模型的逻辑，提升机器学习的算法和模型的zhi在后续对GPT接口的开发中，我们设想可以与Chatgpt进行“人在回路”的系统训练，基本实现我们的设想目标。**



基于"人在回路"的模型训练：

**传统的机器人设计，往往是按照设定好的行为逻辑，这种设计过于机械化。而在医疗领域，传统的机器人显然不足以应对以人为核心的服务化需要。所以我们设想，利用“人在回路“的人机闭环互助系统对机器人进行训练，是否可以使得机器人简单地接近于人类的思维模式。应用在医疗服务等领域**

**人类能够根据实际情况灵活调整策略和方法，这种能力是当前机器人或人工智能难以完全实现的。通过人在回路，机器人在执行任务时可以依据人类的指示灵活调整其行为和策略，更好地适应复杂多变的环境，这就是我们设计的初步思想，虽然从技术的角度出发还有非常遥远的距离，但是我们可以通过这种方法和思想，逐步完善机器人的基本功能。**



==**我们将搭载地平线公司的RDK X3作为主控， 配合32位单片机与各类传感器模块进行数据交互，制作一个能够应用于医疗、后勤等领域的复杂多场景的无人车型机器人，能够先实现以下的基本功能：**==



- 送药：前期阶段实现小车的所有控制部分，通过Opencv，Openmv组成双摄系统。Opencv负责深度学习相关的视觉识别，Openmv通过SPI协议与单片机进行通信，搭建基础的路径检测控制功能。==实现房号识别，自动药物配送。==中期阶段部署利用Simulink或者Gazebo进行小车的运动仿真。

- 自主导航：通过激光雷达进行SLAM建图，使得机器人具备在不同地环境下进行路径规划避障的功能。
- 语言交互：通过API接口与ChatGPT初步实现计算机的文字交互->控制小车基本运动->搭载语音模块控制ChatGPT->完成更复杂的人机交互系统（图像识别+传感器+语音模块）。
- 环境检测：实现小车上述的基本功能后，进行深度学习相关的视觉开发，使用时下热门的YOLO目标检测算法。能够实现对病人如：跌倒检测（识别人体关节点）等视觉应用。

## 队伍信息

**我们队伍命名为FFT队，FFT即为快速傅立叶变换（Fast Fourier Transform），它是一种算法，在信号处理、图像处理、音频处理等领域广泛使用的技术，在如今5G大规模普及的时代，5G具有mMTC(超大规模机器连接)，eMBB(超低延时)的特点，”物联网“，“边缘计算”，“自动驾驶”等技术得到显著的发展。队伍成员基本为为通信系学生。FFT意为我们队伍追求高效、灵活、准确的开发学习，秉持创新思维、以赛促学的思想，能够将创意与专业知识运用在前沿领域。我们希望基于RDK X3 实现一些基于AI与物联网的idea，利用自身的专业知识，能够在本次项目中通信部分进行着重地设计，提高云平台与机器人的通信效率与可靠性。**

