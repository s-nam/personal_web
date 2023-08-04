---
layout: page
title: Setting up a Robotiq 2F gripper and UR10 for Moveit Noetic
author: Saekwang Nam
date: 2023-02-09 14:00:00 +0000
parent: ROS, UR10, Robotiq
grand_parent: Robotics
nav_order: 6
---

# Setting up a Robotiq 2F gripper and UR10 for Moveit Noetic

![Working image](../../../assets/images/Moveit_setup/UR10_with_Rootiq_2F-85.png)

It is worth loading the gripper and the robot arm together in Moveit, because we can easily control its position based on APIs that Moveit provides.

## 1. Condition
- OS: Ubuntu 20.04.5 LTS 64-bit
- Robot: UR10 (CB series)
- Gripper: Robotiq 2F-85
- Moveit: Moveit Noetic

## 2. Helpful websites
- Serru's github ([Go](https://serru.github.io/MultiCobot-UR10-Gripper/docs/moveit-one/))
    > The guideline was based on ROS Kinetic Kame.

## 3. Prerequisite
- You need to have a URDF file in which UR10 is connected to Robotiq 2F gripper. If not, please follow [this](./Create_URDF.md).

## 4. Steps
### 4.1. Launch Moveit! Setup Assistant
```console
$ roslaunch moveit_setup_assistant setup_assistant.launch
```

![Moveit Setup Assistant](../../../assets/images/Moveit_setup/01_MoveIt_Setup_Assistant.png)

### 4.2. Load URDF file
![Load URDF file](../../../assets/images/Moveit_setup/02_Load_urdf.png)

Click "Create New Moveit Configuration Package" and select the URDF file.

### 4.3. Self-Collisions
![Self collisions](../../../assets/images/Moveit_setup/03_Self-Collision_Checking.png)

On the left tabs, click "Self Collisions". On its bottom of the window, click "linear view", and click "Generate Collision Matrix".

### 4.4. Virtual Joints
![Define Virtual Joints](../../../assets/images/Moveit_setup/04_Define_Virtual_Joints.png)

On the left tabs, click "Virtual Joints". Then, click "Add Virtual Joint".

![World joint](../../../assets/images/Moveit_setup/05_world_joint.png)

Type as the above figure shows.

### 4.5. Planning Groups
![Define planning groups](../../../assets/images/Moveit_setup/06_Define_Planning_Groups.png)

On the left tabs, click "Planning Groups". And then, click "Add Group".

![Manipulator](../../../assets/images/Moveit_setup/07_Manipulator.png)

I am going to set two groups. One is "manipulator" and the other is "gripper". Please type as the above figure shows. Next, click "Add Kin. Chain" button.

![Set manipulator's base and tip link](../../../assets/images/Moveit_setup/08_Set_base_and_tip_link_manipulator.png)

Make sure of the manipulator's base link and tip link. Later, click "Save".

![Add group](../../../assets/images/Moveit_setup/09_Add_Group.png)

Next, you need to make the other group for the gripper. Click "Add Group" button.

![Gripper](../../../assets/images/Moveit_setup/10_Gripper.png)

Type as the above figure shows. Then, click ``"Add Joints"``.

![Add finger joint](../../../assets/images/Moveit_setup/11_Add_gripper_finger_joint.png)

Select "gripper_finger_joint". Then, click "Save".

![Final check](../../../assets/images/Moveit_setup/12_Define_Planning_Groups_final.png)

Double-check if your setup is same as the above figure.

### 4.6. Robot Poses

![Robot Poses](../../../assets/images/Moveit_setup/12_Define_Planning_Groups_final.png)

In this step, you can pre-define the poses of the robot. Click "Add Pose".

![Home pose](../../../assets/images/Moveit_setup/13_Home_pose.png)

Make the "home" pose by setting the joint angles. Then, click "Save".

![Gripper open](../../../assets/images/Moveit_setup/14_gripper_open.png)

It is time to pre-defin the gripper. Click "Add Pose" and type as the above figure shows. Then, click "Save".

![Gripper close](../../../assets/images/Moveit_setup/15_gripper_close.png)

Let's pre-define "gripper-close".

### 4.7. End Effectors
![End effector](../../../assets/images/Moveit_setup/16_End_effectors.png)

It is time to define the end-effector. Click "Add End Effector".

![Define eef](../../../assets/images/Moveit_setup/17_Define_end_effectors.png)

Set as the above figure shows. Click "Save".

### 4.8. Passive Joints
The gripper is basically 1 degree of freedom (just from open to close). Therefore, we need to restrict unnecessary movements in the gripper. Because the gripper moves by controlling ``"gripper_finger_joint"``, and the other parts follows as the joint moves. Therefore, we need to set such parts as passive joints.

![Define passive joints](../../../assets/images/Moveit_setup/18_Define_passive_joints.png)

Set as the above figure shows.

### 4.9. Controllers
![Setup controllers](../../../assets/images/Moveit_setup/19_Setup_Controllers.png)

This program will automatically assign the controllers. Click "Auto Add FollowJointsTrajectory..." button.

### 4.10. Simulation
![Gazebo simulation](../../../assets/images/Moveit_setup/20_Gazebo_Simulation.png)

If you click "Simulation" in the left tab, you need to decide if you want to overwrite some codes for Gazebo simulations. I recommend to overwrite.

### 4.11. Author Information
![Author](../../../assets/images/Moveit_setup/21_Author.png)

Include your information.

### 4.12. Configuration files
This program will generate a package so that you can launch the UR10 + gripper in Moveit. 

You first need to create a folder under ``catkin_ws/src``. I set the package name as ``ur10_gripper_moveit``.

```console
~/catkin_ws/src$ mkdir ur10_gripper_moveit
```

![Generate configuration](../../../assets/images/Moveit_setup/22_Generate_configuration.png)

Click "Browse" button and locate the ``ur10_gripper_moveit`` folder. Next, click "Generate Package".

## 5. Lauch Moveit!
You first need to build the catkin workspace.
Locate under ``catkin_ws`` and execute the below.

```console
~/catkin_ws$ catkin_make
```

You can try to launch any predefined files. They are under ``catkin_ws/src/ur10_gripper_moveit/launch``.

I would like to try ``demo.launch``.

```console
$ roslaunch ur10_gripper_moveit demo.launch
```

![Moveit](../../../assets/images/Moveit_setup/23_Moveit.png)

You should see like the above figure. Feel free to move the gripper and manipulator.