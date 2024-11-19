# Drone SLS Controller for ACC-2024: SITL

## I. Install/Getting Started
### 1. Install PX4 Software
```
git clone https://github.com/ANCL/ACC-Repository.git --recursive
bash ./ACC-Repository/Tools/setup/ubuntu.sh
logout
```
login again, and
```
cd ~/ACC-Repository
make px4_sitl gazebo
```
Ctrl + C to kill the terminal upon completion.

### 2. Install ROS Noetic & MAVROS
Follow the guide at https://docs.px4.io/main/en/ros/mavros_installation.html
REMINDER: Do BINARY installation of MAVROS

### 3. Compile ROS Packages
```
cd ~/ACC-Repository/Tools/sitl_gazebo/ancl_sls/RosControl
catkin_make
```
### 4. Install XMLStarlet if not already done
```
sudo apt install xmlstarlet
```
### 5 Install QGroundControl
```
sudo usermod -a -G dialout $USER
sudo apt-get remove modemmanager -y
sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
sudo apt install libqt5gui5 -y
sudo apt install libfuse2 -y
```

Download QGC image
```
wget https://d176tv9ibo4jno.cloudfront.net/latest/QGroundControl.AppImage
```

Install using the terminal commands
```
chmod +x ./QGroundControl.AppImage
```

Enable virtual joystick
<ol>
  <li>Select the Q icon from the top toolbar</li>
  <li>Open the Application Settings</li>
  <li>Make sure you're on the General tab</li>
  <li>Check the Virtual joystick box</li>
</ol>
Refer to QGC guide for more info: https://docs.qgroundcontrol.com/Stable_V4.3/en/qgc-user-guide/settings_view/virtual_joystick.html

## II. Run SITL
### 1. Launch PX4 SITL
```
# in a new terminal
cd ~/ACC-Repository/Tools/sitl_gazebo/ancl_sls
./mavros_script.sh
```

### 2. Run QGroundControl
```
# in a new terminal
cd
./QGroundControl.AppImage
```

### 3. Launch Single SLS Contoller
run the get_states_node
```
# in a new terminal
source ~/ACC-Repository/Tools/sitl_gazebo/ancl_sls/RosControl/devel/setup.bash
rosrun offboardholy get_states_holy_node
```
run the offboard control node
```
# in a new terminal
source ~/ACC-Repository/Tools/sitl_gazebo/ancl_sls/RosControl/devel/setup.bash
rosrun offboardholy offb_control_holy_node
```
