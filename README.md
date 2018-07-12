# autonomous_chair

## Overview

localization of a autonomous chair with cartographer 

**Keywords:** localization, cartographer


The autonomous_chair package has been tested under [ROS] Kinetic and Ubuntu 16.04. This is research code, expect that it changes often and any fitness for a particular purpose is disclaimed.

## Installation

### Installation from Packages

To install all packages from the this repository as Debian packages use

    sudo apt-get install ros-indigo-...

### Building from Source

#### Dependencies

- [Robot Operating System (ROS)](http://wiki.ros.org) (middleware for robotics),

#### Building

To build from source, clone the latest version from this repository into your catkin workspace and compile the package using

	cd catkin_workspace/src
	git clone https://github.com/manuelilg/autonomous_chair.git
	cd ../
	rosdep update
	rosdep install --from-paths src --ignore-src -r -y
	catkin build

## Usage

####How to create a map:

1. Record data while driving in the environment:

        roslaunch autonomous_chair_cartographer record.launch
    
2. Run offline cartographer node (creates .pbstream-file):

        roslaunch autonomous_chair_cartographer offline_chair.launch
    
3. Create map:

        roslaunch autonomous_chair_cartographer offline_map_creation.launch

####Run localisation on a given map:

    roslaunch autonomous_chair_cartographer localisation.launch


####Run a simple simulation of the chair:

    roslaunch roslaunch autonomous_chair_gazebo chair_world.launch


####Visualize the chair and the laser-scan data (real or simulated chair):

	roslaunch autonomous_chair_description rviz.launch


## Launch files

* **record.launch:** Starts rosbag record
    
     Note:

     - bag-file will be saved in the directory from where the launch-file have been started 

* **offline_chair.launch:** start offline slam
    
     Argument set 1

     - **`bag_filenames`** Absolute path to bag-file 
     - **`no_rviz`** Set to false to see the progress of the SLAM-Prozess. Default: `true`.
     
     Note:
     
     - pbstream-file will be in the same directory as the bag-file 

* **offline_map_creation.launch:** start offline slam
    
     Argument set 1

     - **`bag_filenames`** Absolute path to bag-file 
     
     Note:
     
     - the map-files will will be in the same directory as the bag-file/pbstream-file 


* **localisation.launch:** start localisation
    
     Argument set 1

     - **`pbstream_file`** Absolute path to pbstream-file 
     - **`map_file`** Absolute path to map-file (yaml)
     - **`initial_pose`** initial-pose in the given map. \
       Default: `translation={0.0, 0.0, 0.0}, rotation={0.0, 0.0, 0.0}`
       
* **chair_world.launch:** start localisation
    
     Argument set 1

     - **`pbstream_file`** Absolute path to pbstream-file 
     - **`map_file`** Absolute path to map-file (yaml)
     - **`initial_pose`** initial-pose in the given map. \
       Default: `translation={0.0, 0.0, 0.0}, rotation={0.0, 0.0, 0.0}`


## Config files

Config file in dir: autonomous_chair_description/configuration_files

* **chair.lua** cartographer configuration-file for SLAM (settings maybe need to be tuned)
* **chair_localisation.lua.lua** cartographer configuration-file for localisation (settings maybe need to be tuned)


[ROS]: http://www.ros.org
[rviz]: http://wiki.ros.org/rviz
[gazebo]: http://gazebosim.org/
[cartographer]: http://wiki.ros.org/cartographer
[sensor_msgs/Temperature]: http://docs.ros.org/api/sensor_msgs/html/msg/Temperature.html
