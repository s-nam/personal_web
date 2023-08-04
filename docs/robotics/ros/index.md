---
title: ROS, UR10, Robotiq
layout: default
parent: Robotics
nav_order: 2
has_children: true
has_toc: true
# child_nav_order: reversed
---

# ROS, UR10, Robotiq

This section summarizes my know-how in building and controlling a system with a robot and a gripper. The following information is the main environment I have used.
- OS: Ubuntu 20.04
- ROS: ROS 1 Noetic
- Robot arm: UR10 CB-series from Universal Robots
- Gripper: Robotiq 2F gripper for CB-series

Contents
----------------

1. Install URSim on virtual machines ([Go](./2022-12-27-Install_URSim_on_virtual_machine.html))

    > There are two ways to install a URSim simulator using Virtual Box. In particular, you can find out how to correctly set up the network connecting between your main OS and the virtual machine.

2. Control UR robots with Python using CRI ([Go](./2023-01-02-CRI_installation_guide.html))

    > If you want to control the robot using Python codes without using any middle ware (ROS, MoveIt, etc), you can install CRI and run an Python example.

3. Controlling UR arms on ROS Noetic ([Go](./2023-01-11-Install_UR10_on_ROS_Noetic.html))

    > There are instructions and tips in installing ROS Noetic, Moveit, and ROS driver for Universal Robots.

4. Installation of Robotiq 2F gripper ([Go](./2023-01-11-Install_Robotiq_2F_gripper.html))

    > It is quite difficult to find an official way to install/control a Robotiq 2F gripper on ROS Noetic. You can find the know-how that I did.

5. Linking a Robotiq 2F gripper's URDF to UR10's URDF ([Go](./2023-02-07-Create_URDF.html))

    > This tutorial will guide you on how to attach a Robotiq 2F gripper to the end effector of UR10 in the virtual simulation environment.

6. Setting up Robotiq 2F gripper and UR10 for Moveit Noetic ([Go](./2023-02-09-Moveit_setup.html))

    > If you want to load the gripper and the robot arm (UR10) together in Moveit and control the both, please check this.