# Assignment
The task is to create a simulation environment for a Robot in the Gazebo platform, where the robot Navigates around the environment to learn about its environment and will generate a map of its environment

## Installation of ROS and Gazebo on Ubuntu System.
 1.	First of all, installed ROS noetic version in your Ubuntu machine in VirtualBox. Then, check the version of ROS to check if it has been installed properly using the command 'rosversion -d'. 
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

3.	After that, let’s take a look at the ros topics using the command “rostopic list’ as shown below.
![turtlesim(2)keyboard_teleop](https://user-images.githubusercontent.com/83338844/182208441-34d359a4-470c-4573-b49d-d2ef74539a3b.png)
As we can see, the publisher ‘/turtle1/cmd_vel’ is used in the code to control the turtlebot.

4.	Now, Let’s modify the code accordingly and execute the code using the command ‘rosrun turtle_one turtle_keyboard.py’. The control instructions are shown in the picture below.
![turtlesim(3)_teleop_keyboard](https://user-images.githubusercontent.com/83338844/182208760-290263d7-00a4-4f1b-90da-5c5a885c3303.png)

### (Now using TurtleBot3)
5.	Now, in the same way, Let’s use the same code for keyboard control on the TurtleBot3 as depicted in the figure. Here, the publisher ‘/cmd_vel’ is used in the code.
![turtlebot3(1)keyboardcontrol](https://user-images.githubusercontent.com/83338844/182208986-f79b8cfe-95ae-432b-a811-6399d604adf1.png)

![turtlebot3(2)keyboardcontrol](https://user-images.githubusercontent.com/83338844/182209020-fab46cdd-c2e5-49c1-b991-3c65ec7a5ad3.png)
