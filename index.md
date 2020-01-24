# Mobile Robot Course

I have already summarized the content to bring up the Turtlesim.

## Setup environment

Ref. http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment

## Create package
Before create the new package, the current folder must be `~/catkin_ws/src`.
```
cd ~/catkin_ws/src
catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```

Now you need to build the packages in the catkin workspace.
Before build, the current folder must be `~/catkin_ws`.

```
cd ~/catkin_ws
catkin_make
```


Ref. http://wiki.ros.org/ROS/Tutorials/CreatingPackage

## Run Turtlesim Node
Ref. http://wiki.ros.org/ROS/Tutorials/UnderstandingNodes


## Run Teleop Node and publish topic

Ref. http://wiki.ros.org/ROS/Tutorials/UnderstandingTopics

## Control turtlesim using Python
Ref. http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29
