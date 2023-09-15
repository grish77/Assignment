# Task
The task is to create a simulation environment for a Robot in the Gazebo platform, where the robot Navigates around the environment to learn about its environment and will generate a map of its environment

## Installation of ROS and Gazebo on Ubuntu System.
 1.	First of all, Let's install the ROS noetic version in your Ubuntu machine. Then, check the version of ROS to check if it has been installed properly using the command 'rosversion -d'. 
![ros install](https://user-images.githubusercontent.com/83338844/182037660-8d0d8811-5023-460c-91ec-0b9d8161d346.png)
 2.	After that, check if the standalone Gazebo is working properly and check the version of Gazebo using command 'gazebo --version'. Then, try to start gazebo using the roslaunch command 'roslaunch gazebo_ros empty_world.launch'. This is shown in the image below.
![gazebo test](https://user-images.githubusercontent.com/83338844/182037625-f28a22eb-eb5b-4445-a533-76b907d235cf.png)
3.	Then, install rviz (ROS Visualization) using the command ‘sudo apt-get install ros-noetic-rviz’ (for noetic distro). To startup the visualizer run the command ‘rosrun rviz rviz’ as shown in the diagram below.
![rviz launch](https://user-images.githubusercontent.com/83338844/182207634-22efbe19-c4a8-4106-a998-74ac0bb8dc3a.png)

## Custom ROS Package for keyboard teleoperation by publishing commands to topic /cmd_vel

1.	To create a custom ROS package in the catkin workspace, first go to catkin workspace folder using the command ‘cd catkin_ws/src/’ and to create a package, use command ‘catkin_create_pkg <package_name> rospy roscpp std_msgs gazebo_ros’. After that, come out of the src folder using ‘cd ..’ command and use command ‘catkin_make’. If the catkin_make is successful, the package is successfully created. 
![Creating a Package](https://user-images.githubusercontent.com/83338844/182207853-8ac43be9-a63a-420d-a15f-901e4fdf59ee.png)

2.	For this purpose, first run the roscore and then start the turtlesim using the command ‘rosrun turtlesim turtlesim_node’ as shown in the figure below.
![turtlesim(1)keyboard_teleop](https://user-images.githubusercontent.com/83338844/182208162-edb788f7-37c9-49f5-9d9e-2541adabad1a.png)

3. After that, in a new terminal, let’s take a look at the ros topics using the command “rostopic list’ as shown below.
![turtlesim(2)keyboard_teleop](https://user-images.githubusercontent.com/83338844/182208441-34d359a4-470c-4573-b49d-d2ef74539a3b.png)
As we can see, there is a topic called ‘/turtle1/cmd_vel’ that we are going to use to publish the velocity commands to control the turtlebot using keyboard.

4.	To control the turtle bot, the teleop_twist_keyboard package can be directly installed using the command ‘sudo apt-get install ros-noetic-teleop-twist-keyboard’ and use the command ‘rosrun teleop_twist_keyboard teleop_twist_keyboard.py’. However, in this case, the open source python code for keyboard control has been used with slight modification, creating our own package ‘turtle_one’. Now, Let’s modify the code accordingly and execute the node in a new terminal using the command ‘rosrun turtle_one turtle_keyboard.py’. The control instructions are shown in the picture below.
![turtlesim(3)_teleop_keyboard](https://user-images.githubusercontent.com/83338844/182208760-290263d7-00a4-4f1b-90da-5c5a885c3303.png)

### (Now using TurtleBot3)
5.	Now, in the same way, Let’s use the same code for keyboard control on the TurtleBot3 as depicted in the figure. Here, the topic ‘/cmd_vel’ is used to publish the motion commands in the code.
![turtlebot3(1)keyboardcontrol](https://user-images.githubusercontent.com/83338844/182208986-f79b8cfe-95ae-432b-a811-6399d604adf1.png)

![turtlebot3(2)keyboardcontrol](https://user-images.githubusercontent.com/83338844/182209020-fab46cdd-c2e5-49c1-b991-3c65ec7a5ad3.png)

## Offline Loading and Visualization of the map on RViz environment

1.	Let’s start with installation of the Simultaneous Localization and Mapping (SLAM) module. This module takes care of building robot and updating map in an unknown environment as well as keeps track of the location at the same time. Use installation command ‘sudo apt install ros-noetic-slam-gmapping). The gmapping package helps in creating a 2-D occupancy grid map. Here, all the packages needed for this purpose have been git cloned using the link ‘https://github.com/ROBOTIS-GIT/turtlebot3.git’.
![SLAM module installation](https://user-images.githubusercontent.com/83338844/182410436-b51f090a-e462-41a5-b247-5a44a9144508.png)

2.	Now, in another terminal. Launch the gazebo world for our simulation using the command ‘roslaunch turtlebot3_gazebo turtlebot3_world.launch’
![Gazebo launch](https://user-images.githubusercontent.com/83338844/182410827-97998022-8c63-4cd2-938a-fa22caf54f40.png)

3.	After that, for mapping purpose, launch another node in a new terminal using command as shown below.
![SLAM launch](https://user-images.githubusercontent.com/83338844/182411006-6fe287f6-377f-442b-a9db-7c4b20960454.png)

4.	Again, in a new terminal, start Autonomous Navigation.
![Auto nav launch](https://user-images.githubusercontent.com/83338844/182411214-a2c08316-9e49-49de-b22e-00de70f43c0f.png)
As we can see, the map of the gazebo environment is being created in the rviz environment as the turtlebot moves around autonomously.
![Auto nav map creation](https://user-images.githubusercontent.com/83338844/182411437-ed71f7cc-f426-485c-8198-fca3161b7208.png)

5.	Once the desired map is created, the map can be saved. Let’s get inside the catkin workspace and then in src folder, where we are going to create a folder called maps to store the map. Then, go inside the maps directory and run the command ‘rosrun map_server map_saver –f  rviz_map’ . This command creates two files in the maps directory called rviz_map.pgm and rviz_map.yaml and they contain information about the map.
![creating folder for map](https://user-images.githubusercontent.com/83338844/182411672-7261e0a3-c8ac-4156-aaac-5bbd9159f65b.png)
Now, we can close all the terminals that are running.

6.	Now, to open the saved map, go to the catkin_ws/src/maps/ and execute the command ‘rosrun map_server map_server rviz_map.yaml’. and again launch rviz to view the map. Make sure you have the correct map topic as shown in the figure.
![opening the map](https://user-images.githubusercontent.com/83338844/182412227-4a81837a-76d7-41dd-b79a-cb60c83e91bb.png)
![offline map in rviz](https://user-images.githubusercontent.com/83338844/182412329-2d227d6b-c809-4244-90f3-afe5b5162bb2.png)

## Simulating a Customized Robot by creating custom URDF file on Gazebo

Let’s start by making a package named my_robot using the command ‘catkin_create_pkg my_robot rospy roscpp std_msgs’ and then add or make necessary folders inside the package using the command ‘mkdir’. Start with creating a folder called urdf, where we are going to add our urdf file. We can make any file inside a directory using the command ‘touch filename.extension’ and make it executable using ‘chmod +x filename.extention’ command. To edit any file, we can use the command ‘gedit filename.extention’. We also need other folders like launch and world, where we create our launch file and world file for successfully simulating our customized robot in gazebo world. All the files have been added to the git repository.

Different files needed for the creation of custom robot are described below.
1.	URDF file
The term URDF stands for Universal Robotic Description Format and follows XML format for description of different components of any model. Different parts of any URDF file are:

a.	Links: 

A link is a part of a robot and has multiple aspects like inertial, collision, and visual aspect. The inertial aspect contains the properties of any link such as link’s mass, position of its center of mass, and its central inertia. The collision aspect of any link specifies the geometrical properties of the link. The visual aspect of a link has the visual properties of link and makes the link visible.
![link_urdf](https://user-images.githubusercontent.com/83338844/183009696-83533c9a-06e8-4c0e-98b7-4d3851c04756.png)

b.	Joints:

Two links or parts of any model or robot are connected using joints. The joint element describes the kinematics and dynamics of the joint. The attribute name specifies the name of the joint and type specifies the type of joint.
![joints](https://user-images.githubusercontent.com/83338844/183009714-6cc1fbdb-94f9-4c78-b10b-f4d9de6d205a.png)


2.	Gazebo Plugin (filename.gazebo)

The gazebo plugin defines how does the controller actually get plugged in and how the control commands are published. It is wrapped in with <gazebo> pill to indicate the information passed to gazebo. Gazebo plugins give URDF models greater functionality and can tie in ROS messages and services for sensor output and motor input.
![gazebo plugin](https://user-images.githubusercontent.com/83338844/183009726-b45b757e-2a92-4f19-aa55-75481cb7e1c0.png)
 
 3.	Launch files: 
 
Launch files are needed to launch the custom model or spawn the model. There are two launch files in for our model, world.launch and robot_description.launch. 
![world_launch](https://user-images.githubusercontent.com/83338844/183009750-b5d5b68e-a2bc-4e5c-98d4-bb8cb9b7d7fd.png)

 ![robot_des_launch](https://user-images.githubusercontent.com/83338844/183009771-795e7cdd-d986-44d0-85cd-24e740a41110.png)
 
 4.	World file
 
A world file is a file that contains the information or description of all the elements like robots, lights, sensor, etc. to be simulated in gazebo.
![empty_world](https://user-images.githubusercontent.com/83338844/183009819-b5906686-f87a-464d-a20d-156b79b4f19b.png)


After creation of all the files, it is time to launch our custom robot in the gazebo world. It can be done in the following steps:
 
 1.	Go to catkin_ws and run ‘catkin_make’ command to build the packages in catkin_ws and source the setup.sh file for adding environment variable.
 ![first_custom](https://user-images.githubusercontent.com/83338844/183009793-acac7df9-788a-411f-b7a9-bab9b66a5958.png)

 2.	Launch the robot in gazebo world using command ‘roslaunch my_robot world.launch’.
 ![second_custom](https://user-images.githubusercontent.com/83338844/183009846-369dd629-9d90-4f70-96a1-eeb89ec17af4.png)

 3.	We can see our robot in the empty gazebo world now. Using our code for keyboard control that we created earlier, we can control our robot.
 ![3rd_custom](https://user-images.githubusercontent.com/83338844/183009856-0c2500a3-97d3-475e-b185-46042742bf87.png)

