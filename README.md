# Visual-Servoing-using-ROS-and-Gazebo

This is a quick setup guide and introduction to Robot Operating System (ROS) and Gazebo. Using these tools visual servoing has been demenstrated with marker identities on bots.

## Introduction
A typical robotic system is equipped with sensors, actuators, motors etc. along with com-
puting unit which can either take instructions from a user or it can also act autonomously
depending on the application for which it is designed and the modeling of the software
components that’s driving the computing unit.
The computing unit can be a full-fledged general purpose computers and also for small
robotic and less computing power requirement applications, SBCs can also be used such
as Raspberry Pi, Nvidia Jetsons, Arduino boards etc.
Once hardware computing unit is figured out we need to have a software framework
upon which the interaction through hardware will be possible for sensor inputs, analyzing
the data and producing action-outputs through actuators and motors. This framework is
available to us by open source community known as Robot Operating System.
ROS along with tools that comes along with like likes of rviz, rqt, gazebo etc gives a
complete package of testing out codes, running simulations in real time without the need
of having actual hardware-based robotic system.
Therefore the initial phase of this project focused more on understanding the concepts
of ROS and various libraries and tools that accompanies it. Once the whole structure
and working of ROS is understood, then the next step it to model the system to take
feed from various sensors, train and learn the environment with one of RL algorithms 
on reward/cost basis and take the rightful action depending upon the application for
which the system is designed. Specifically the focus will be to model a robot using URDF
which will have main camera sensor accompanied by other sensors and program it either
in Python or C++ for the implementation of RL algorithm and using computer vision
libraries (Ex. OpenCV) to perform visual servoing in an environment.

## Robot Operating System (ROS)
The official definition of ROS gives us insight into its capabilities, functionalities and ser-
vices framework upon which we can build our robotic system :
”ROS is an open-source, meta-operating system for your robot. It provides the services
you would expect from an operating system, including hardware abstraction, low-level de-
vice control, implementation of commonly-used functionality, message-passing between
processes, and package management. It also provides tools and libraries for obtaining,
building, writing, and running code across multiple computers.”
Here ”meta OS” means that it runs on top of a full OS such as Ubuntu(Linux), like
we can have RPi or JNs SBCs which both runs on Linux and can be easily integrated and
used as a robot computing unit and what ROS will do is to provide all the software’s tools
and packages for response, reception and interaction capability through programming. So
in essence ROS sits on top of Linux together which acts like fully functional brain for a
robot.

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219786746-5cf3519a-b2af-46d7-93a7-bb6935ce9b91.png" width="70%" />
</p>

ROS architecture and implementation is build on modular concepts meaning the parts
of the system are separated as per their functionality and they communicate via different
types of messages in different pipelines.

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219786540-04ce5d66-691a-4a11-a231-680c65b61d02.png" width="70%" />
</p>

Various terminologies and concepts regarding the above architecture is covered as
below :  

• **ROS nodes**: Process that use ROS APIs to perform computations.  
• **ROS master**: An intermediate program that connects ROS nodes.  
• **ROS parameter server**: A program that normally runs along with the ROS master.
The user can store various parameters or values on this server and all the nodes
can access it. The user can set privacy of the parameter too. If it is a public
parameter, all the nodes have access; if it is private, only a specific node can access
the parameter.  
• **ROS topics**: Named buses in which ROS nodes can send a message. A node can
publish or subscribe any number of topics.  
• **ROS message**: The messages are basically going through the topic. There are
existing messages based on primitive data types, and users can write their own
messages.  
• **ROS service**: We have already seen ROS Topics, which is having publishing and
subscribing mechanism. The ROS Service has Request/Reply mechanism. A service
call is a function, which can call whenever a client node sends a request. The node
who create a service call is called Server node and who call the service is called client
node.  
• **ROS bags**: A useful method to save and play back ROS topics. Also useful for
logging the data from a robot to process it later.  

To understand ROS completely with actual implementation we will go through the following sections :  
• ROS installation    
• ROS tools  
• ROS commands  
• URDF  

### ROS Installation
ROS installation process and prerequisites are covered in following points :

• The following combination of OSs and software packages are required for the current
project to work on – Ubuntu 16.04 + ROS Kinetic + Gazebo7.  
• Upon following the official procedure linked below for ROS Kinetic installation will
automatically install rviz, rqt and Gazebo7.  
• Official installation link and guide -http://wiki.ros.org/kinetic/Installation/
Ubuntu  
• Upon installation check the ROS version with following command in the terminal `rosversion -d`
• Check Gazebo version by opening Gazebo with the command`gazebo` and then
clicking on ‘About’ tab in Gazebo GUI.  
• Check rviz installation with command `rosrun rviz rviz`  
• Check rqt installation with command `rosrun rqt gui rqt gui`  

After above steps the ROS setup is complete.

### ROS tools
Here are the basic tools that is used under ROS :

• **rviz**  
It stands for ROS Visualization. It’s a 3-dimensional visualization tool for ROS. In
essence it helps in visualizing what the robot is seeing and doing through various
sensors data.

*Command to open* - `rosrun rviz rviz`

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219786345-705bea42-af33-4b08-b9d0-3552420848ca.png" width="70%" />
</p>

• **rqt**  
rqt is a software framework of ROS that implements the various GUI tools in the
form of plugins. It helps to visualize 2D data, logging topics, publishing topics,
calling services etc.

*Command to open* - `rosrun rqt gui rqt gui`

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219786240-f62c14cc-4ea8-489f-b2bf-aae070e2fd3e.png" width="70%" />
</p>

• **Gazebo**  
It’s a robotic simulator used with ROS. It is used for desiging and modeling environ-
ments and robots in 3D world, perform testing of algorithms and train AI system
using realistic scenarios. Gazebo has a physics engion under the hood, high-quality
graphhics and also easy to use GUI.

*Command to open* - `gazebo`

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219786160-2bdbc0d3-860a-4010-aad6-ea94886a8b23.png" width="70%" />
</p>
      
### ROS commands  
• **roscore** - it starts the ROS master, the parameter server, and a logging node.  
• **rosnode** – everything to do with a ROS node.  
• **rostopic**- provides information about the topics  
• **rosservice**- provides information about ROS services  
• **rosparam**- listing, setting and getting parameter values  

### URDF  
The Unified Robotic Description Format (URDF) is an XML file format used in ROS to
describe all elements of a robot.

Various links, different kinds of joints, physical properties like inertia, collisions etc,
visual appearance and other dynamics are defined.
To be compatible with the Gazebo simulator, plugins are used. The typical URDF
format for a robot has following XML structured file :

```
<?xml version="1.0"?>
<robot name="ROBOT A">
<link name="base_link">
<visual>
<geometry>
<cylinder length="0.6" radius="0.2"/>
</geometry>
</visual>
</link>
</robot>
```

As we can see from the XML file above there are various sections defined like links,
visual, geometry etc. to model our robot as per our requirement and use-case.

## Visual Servoing
Visual servoing is a term which is exclusively used in robotics world where the feed from
camera sensor are fed into the robot which is then used to gather relevant information
and subsequently plan the motion of the robot.
To perform visual servoing in a conventional way the first task is to have two robots in
the simulated world and make one robot follow another which has some kind of visually
identifiable marker attached to it.
All the discussion and scenarios will be executed in a simulated world in Gazebo. We
will have a world to explore, two robots autonomously navigating this world and to one
of the robot a marker will be attached which the other robot will follow through the video
feed.
The models for robots, environment and other objects are defined in ”XML” files.

Modeling the marker
So we can have a visual marker defined as follows :

```
<?xml version="1.0"?>
<sdf version="1.6">
<model name="aruco_marker">
<link name="link">
<inertial>
<pose>0 0 0 0 0 0</pose>
<mass>0.001</mass>
<inertia>
<ixx>3.7499999999999997e-06</ixx>
<ixy>0.0</ixy>
<ixz>0.0</ixz>
<iyy>1.8750008333333333e-06</iyy>
<iyz>0.0</iyz>
<izz>1.8750008333333333e-06</izz>
</inertia>
</inertial>
<visual name="front_visual">
<pose>0.00005 0 0 0 0 0</pose>
<geometry>
<box>
<size>0.0001 0.15 0.15</size>
</box>
</geometry>
<material>
<script>
<uri>model://aruco_marker/materials/scripts</uri>
<uri>model://aruco_marker/materials/textures</uri>
<name>Marker</name>
</script>
</material>
</visual>
<!-- Hide the marker from the back -->
<visual name="rear_visual">
<pose>-0.00005 0 0 0 0 0</pose>
<geometry>
<box>
<size>0.0001 0.15 0.15</size>
</box>
</geometry>
</visual>
<collision name="collision">
<pose>0 0 0 0 0 0</pose>
<geometry>
<box>
<size>0.0001 0.15 0.15</size>
</box>
</geometry>
</collision>
</link>
</model>
</sdf>
```
<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219785837-deff19e6-6e3c-45e9-bb8b-7b68be2d846d.png" width="50%" />
</p>

The above definition in XML file defines the visual appearance in 3D world and its
physical properties like positions, dimensions and how it interacts with the environment
are all defined.

### Attaching the marker to a robot
Now once we have our marker model ready we need to attach it to a robot. Gazebo has
a plugin called ” gazebo ros link attacher ” that helps in attaching two models de-
fined in Gazebo together. To successfully attach the marker to the robot we need to have
initial pose the robot estimated during simulation. So before the start of the simulation
we need to run a script that will pause the simulation for a moment, estimate the pose of
the robot and attach the marker to this estimated pose, then we resume to the simulation.

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219785616-ddbf28c7-b6ff-49cb-9aeb-9a04f4ad5c65.png" />
</p>

### Visual servoing
Now since we have our robot (let’s name it Robot A) with its marker attached roaming
in the environment, we need an algorithm for the other robot (Robot B) to follow it by
tracking the marker.

### Algorithm :
1. Since we have used ArUco marker on robot A, the robot B uses aruco.detect package
to subscribe to camera topic and scans for marker images in it.  
2. Once the marker is detected the node publishes the 3D transformations.  
3. This 3D transformation and marker ID tells the robot B the position and orientation of
the marker (and hence the robot A location) w.r.t camera.  
4. The vision based control closed feedback algorithm that will be applied here will maintain a certain relative position w.r.t the target.  
5. The closed loop control feedback functions as follows :  
  * if marker is not detected
    * if enough time has passed, start exploration  
  * if marker is detected
    * if exploration is in progress, cancel exploration
    * compute global navigation goal
    * send navigation goal
6. Target following :  
  • move to a vantage point where we can expect the target to appear  
  • rotate in place 360 degrees to observe the space all around  
7. The transformations required to achieve the final goal of getting the required pose of
the robot A starting from reception of marker data is shown below :

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219789018-a4b6de0b-b881-4d26-9024-db78b1274abf.png" width="50%" />
</p>

Here :  
$T_{cf}$ : Marker transformations  
$T_{mt}$ : Navigation goal for robot B  
$T_{rc}$ : Robot to camera transformation  
$T_{mr}$ : Map to robot transformation  

## Result
As we can see from the rviz gui tool, from the robot B point of view of camera, it has
detected the marker attached to the robot A. So it has marked the position of that at
the time of interception and has re-routed itself to the new location. Also as we can see
the target robot A is on its move to a different location as it is roaming freely in the
environment.
Once this current target position is reached, the robot B again starts intercepting the
camera feed and looks for the marker by spanning 360°or by moving to a vantage point
to extend the point of view. This process continues until halted otherwise.

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219783507-36573c5c-c444-4b2b-babe-2cddd9d3bf0e.png" width="70%" />
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219783566-fe82db4e-36d0-449d-acb5-7bad050bad38.png" width="70%"/>
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/71163637/219783792-43dd34d0-32f1-46e0-bf75-d1ec7c4bbb7d.png" width="70%"/>
</p>


## References  
[1] Lentin Joseph. Robot Operating System for Absolute Beginners: Robotics Programming  
Made Easy. Apress, 2018.
[2] Nick Lamprianidis. Visual Servoing in Gazebo. - https://nlamprian.me/blog/software/ros/2020/01/27/visual-servoing-in-gazebo/. nlamprian blog, 2020.  
[3] ROS wiki, - http://wiki.ros.org  
[4] Gazebo tutorials, - http://gazebosim.org/tutorialsg  


