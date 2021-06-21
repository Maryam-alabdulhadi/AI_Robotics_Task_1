# AI_Robotics_Task_1

1’st Main Task in AI & Robotics.
Note: download the attached video to be able to view it. 

**Brief Description:**
In this task I will explain how I did the following:
- Downloading VirtualBox.
- Downloading Ubuntu.
- Downloading ROS.
- Create a Workspace.
- Add dependencies.
- Run RIVZ.
- Arduino IDE Linux Version 64-bits.
- Arduino IDE Setup on Ubuntu.
- Download libraries
- Download and run Gazebo  
- Download MoveIt.
- Open RVIZ and Gazebo and Controlling the motors in simulation
- Errors I've faced and how I fixed them


**Downloading VirtualBox:**
-	First, I installed Virtual Box on Windows host through their website and followed the installation steps.

**Downloading Ubuntu:**
-	I Downloaded Ubuntu 18.04 LTS on Virtual Box, Desktop Image 64-Bits PC (bionic) 
-	Then I created a virtual machine of type Linux Version Ubuntu-64-Bits. 
-	Then from the virtual box: Settings  Storage  CD Empty Choose the Ubuntu iso file that I have downloaded before. 
-	Started running the Ubuntu 18.04 Virtual machine and followed the basic installation steps & created an Ubuntu Account. 
-	 After that I went to the next step which is Installing of ROS Melodic on Ubuntu 
-	First, I Configured my Ubuntu repositories to allow "restricted," "universe," and "multiverse”. from the settings 

**Downloading ROS:**
**I used the following codes in the terminal of Ubuntu 18.04:**
-	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
-	curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -


**Error curl command not found so I solved it with:**
-	sudo apt install curl
-	sudo apt update
-	sudo apt install ros-melodic-desktop-full
-	echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
-	source ~/.bashrc
-	sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
-	sudo apt install python-rosdep
-	sudo rosdep init
-	rosdep update


**To check everything is done in ROS setup environment:**
-	printenv | grep ROS


**Create a Workspace:**
-	pwd 
-	source /opt/ros/melodic/setup.bash
-	mkdir -p ~/catkin_ws/src


**To check catkin is created:**
-	ls


**Then:**
-	cd ~/catkin_ws/
-	catkin_make
-	source devel/setup.bash


**This code will show me the path where the workspace is installed, and the type is melodic:**
-	echo $ROS_PACKAGE_PATH


**The following codes is to check roscore runs:** 
-	roscore 
-	rosenode list 
-	rosetopic list 

Download arduino_robot_arm package from S-M GitHub: 
-	cd ~/catkin_ws/src
-	sudo apt install git
-	git clone https://github.com/smart-methods/arduino_robot_arm 

**Add dependencies:**
-	cd ~/catkin_ws
-	rosdep install --from-paths src --ignore-src -r -y
-	sudo apt-get install ros-melodic-moveit
-	sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-   publisher-gui
-	sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
-	sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control


**To prevent the error that says “[check_motors.launch] is neither a launch file in package …etc” I used this code :**
-	sudo nano ~/.bashrc


**At the end of the (bashrc) file I add follwing line:**
-	(source /home/maryam/catkin_ws/devel/setup.bash)


**Then ctrl + o then press Enter, then ctrl + x**
-	source ~/.bashrc
-	roslaunch robot_arm_pkg check_motors.launch


**Run:**
-	roslaunch robot_arm_pkg check_motors.launch


**After I run this code RVIZ Opened up and showed me the robot arm where I can control it!**


**Download Arduino IDE Linux Version 64-bits inside the Ubuntu 18.04 and followed the   installation steps from the link: https://www.arduino.cc/en/software**


**Arduino IDE Setup on Ubuntu + download libraries were downloaded from the source because the installing the binary didn’t work with me, so I used the following codes:**
-	cd ~/catkin_ws 
-	cd src 
-	git clone https://github.com/ros-drivers/rosserial.git
-	cd ..
-	pwd
-	catkin_make 
-	catkin_make install
-	pwd 
-	cd .. 
-	cd ..
-	pwd
-	ls
-	cd home 
-	cd maryam 
-	ls
-	cd Arduino 
-	ls 
-	cd libraries 
-	pwd 
-	clear
-	pwd 
-	rm -rf ros_lib
-	rosrun rosserial_arduino make_libraries.py .


**Restart Arduino and restart Ubuntu then ros_lib appeared on Arduino.**

**Controlling the motors in simulation between Gazebo & RIVZ:**
-	roslaunch robot_arm_pkg check_motors.launch
-	roslaunch robot_arm_pkg check_motors_gazebo.launch
-	rosrun robot_arm_pkg joint_states_to_gazebo.py


**To change the permission**
-	cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
-	sudo chmod +x joint_states_to_gazebo.py


**error “ [Err] [REST.cc:205] Error in REST request “ appeared so I fixed it following this tutorial https://youtu.be/ftDz_EVoatw**
-	basically api.ignitionfuel caused the error. so, I replaced it with api.ignitionrobotics and the error stopped occurring 


**Download MoveIt**
-	roslaunch moveit_setup_assistant setup_assistant.launch
-	roslaunch moveit_pkg demo.launch


**Finally, to opened RVIZ and Gazebo and Controlling the motors in simulation I tried those following codes and it worked!**
-	roslaunch robot_arm_pkg check_motors.launch
-	roslaunch robot_arm_pkg check_motors_gazebo.launch
-	rosrun robot_arm_pkg joint_states_to_gazebo.py


**Thank you for reading:).**
