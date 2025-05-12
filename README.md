# Autonomous Drones with ROS
###### <h6 align="right"> - A group project by Milena Eisemann, Samyak Jain, Abhinav Utkarsh, Fabienne Greier from TU - Munich</h6>


## Table of Contents

1. [Introduction](#introduction)
2. [Video](#video)
3. [Test Bench Hardware](#test-bench-hardware)
4. [RQT - Graph](#rqt---graph)
5. [Setup and Installation](#setup-and-installation)
6. [Running the Project](#running-the-project)
7. [State Machine](#state-machine)
8. [Current Problems](#current-problems)

---

## Introduction

In the summer semester of 2023, we took a course at TU Munich called [Introduction to ROS](https://campus.tum.de/tumonline/pl/ui/$ctx/wbLv.wbShowLVDetail?pStpSpNr=950572887). As part of this course, we were assigned with a project that involved the following components (See the visual overview ![here](../main/documentation/overview.jpg)):

1. **Unity Simulation Environment:** A base version was provided, which we were free to adjust and improve.

2. **ROS-Simulation-Bridge:** This feature served as the communication bridge between the simulation and other ROS nodes via TCP. Again, a base version was provided to us, but we had the flexibility to make any necessary adjustments.

3. **Quadrotor Controller:** This component enabled position control of the drone. As with the other parts, a basic version was supplied, but we could modify it as required.

4. **State Machine:** we had to manage the state machine for our drone, which controlled tasks such as takeoff, exploring, and landing at the specified location.

5. **Perception Pipeline:** This required us to convert the depth image, firstly to a point cloud and then to a voxel-grid representation of the environment.

6. **Path Planner:** We were tasked with creating a path planner that would generate a path through the environment to the goal location.

7. **Trajectory Planner:** Following the path planner, we also had to design a trajectory planner based on the path found.

The path- and trajectory-planning is implemented in 2D by collapsing all obstacles into the x-y plane.

One of the requirements of the project was to implement a custom message or service definition which we did for our state_machine. The detailed documentation can be found in the documentation directory.

## Video

<p align="center">
  Watch our demo video below:
</p>

<p align="center">
  <a href="https://youtu.be/I9YYYC3NxW4">
    <img src="http://img.youtube.com/vi/I9YYYC3NxW4/0.jpg" alt="Project video">
  </a>
</p>

## Test Bench Hardware

This project was implemented and tested on a system running Ubuntu 20.04 with ROS Noetic Full Desktop installed. The specific hardware specifications of the system (a Razer Blade 14 2021 model) are as follows:

- Processor : AMD Ryzen 9 5900X
- Processor Cores: 8
- Memory Size: 16 GB
- Memory Speed: 3200 MHz
- Graphics Card : RTX 3070

All the drone flight tests were performed on this system within a virtual environment running Ubuntu 20.04 with 6 cores and 12GB of Memory.


## RQT - Graph
<p align="center">
  <img src="https://gitlab.lrz.de/00000000014AC757/group_4/-/raw/Revert_Integrate/documentation/rosgraph.svg" alt="rosgraph">
</p>

## Setup and Installation
We were following the instruction doc: Ubuntu Installation Guide (https://docs.google.com/document/d/1HaGEXkqa_M8hBGSx2cSsKWAnSgEtfGKO1poNUynt7DE/edit). 


Install ros-noetic-desktop-full as a base.

Then install the required ROS packages:
single command : 
```
sudo apt-get install python3-catkin-tools ros-noetic-costmap-2d ros-noetic-move-base-msgs ros-noetic-move-base ros-noetic-pointcloud-to-laserscan ros-noetic-explore-lite ros-noetic-octomap-server ros-noetic-rtabmap-ros ros-noetic-rotate-recovery ros-noetic-octomap-rviz-plugins
```


Finally, make sure the two drone files from the course instructor have the right permissions to execute in the 'devel/lib/simulation' folder.

Then finally run
```
catkin build
```
and
```
source devel/setup.bash
```

## Running the Project

To start all the required processes including the Unity simulation and rviz, simply use the launchfile `group4.launch` in the src directory.
```
roslaunch src/group4.launch
```

6.2 Recording & Playback

We use Rosbag for recording and playback, but need to rename the bagfile to recording.bag in the workspace.
Commands: 
play: roslaunch simulation playback.launch
record: rosbag record -a -o recording.bag

## State Machine

The state machine is a wrapper guiding the drone to change the states as shown here:
<p align="center">
  <img src="https://gitlab.lrz.de/00000000014AC757/group_4/-/raw/main/documentation/overview.jpg" width="500" alt="Project Overview">
</p>

## Current Problems
- Lizard Problem
- Elastic controller maneuver
- Confiscated pointclouds on each other
- Sparse 2D scan
- Unexplored regions because of high inflation radius
