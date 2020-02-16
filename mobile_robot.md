
> **ประกาศ**
> 
> ข้อสอบวันที่ 1 [https://forms.gle/e2Vf4mMunzttigtq9](https://forms.gle/e2Vf4mMunzttigtq9)
> ข้อสอบวันที่ 2 [[https://forms.gle/AZibHPiitbRhypGY8](https://forms.gle/AZibHPiitbRhypGY8)
> 

# Mobile Robot Training (Sample code and Command)

## Navigation
* [การสร้าง workspace](#การสร้าง-workspace)
* [การสร้าง package](#การสร้าง-package)
* [การสร้างสคริปท์ภาษา Python](#การสร้างสคริปท์ภาษา-Python)
* [โค้ดตัวอย่างการควบคุมความเร็ว TurtleSim ด้วย Publish](#sample-code-publish-command-velocity-to-control-turtlesim)
* [โค้ดตัวอย่างการควบคุมความเร็ว TurtleBot ด้วย Publish และ Subscribe](#publish-and-subscribe-turtlebot)

## การสร้าง Workspace
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws && catkin_make
```

## การสร้าง package
```
cd ~/catkin_ws/src
catkin_create_pkg my_turtlebot std_msgs rospy roscpp
cd ~/catkin_ws && catkin_make
```
** ห้ามลืม `catkin_make` หลังจากสร้าง package ใหม่ครับ

## การสร้างสคริปท์ภาษา Python
```
cd ~/catkin_ws/src/my_turtlebot
mkdir scripts
touch control_turtlebot.py
chmod +x control_turtlebot.py
cd ~/catkin_ws && catkin_make
```

** คำสั่ง `touch` ใช้สำหรับสร้างไฟล์เปล่า
** chmod +x ใช้สำหรับแก้ไข file permission


## [Sample Code] Publish command velocity to control TurtleSim

```Python
#!/usr/bin/env python
import rospy
from geometry_msgs.msg import Twist

def main ():
    rospy.init_node('listener', anonymous=True)
    rate = rospy.Rate(10) # 10 Hz
    pub = rospy.Publisher('/turtle1/cmd_vel', Twist, queue_size=10)
    velocity_msg = Twist()
    velocity_msg.linear.x = 0
    velocity_msg.linear.y = 0
    velocity_msg.linear.z = 0
    velocity_msg.angular.x = 0
    velocity_msg.angular.y = 0
    velocity_msg.angular.z = 0
    
    i = 0
    while not rospy.is_shutdown():
        # TODO
        velocity_msg.linear.x = 1
	
        
        i += 1
        # END
        pub.publish(velocity_msg)
        rate.sleep()
        
if __name__ == '__main__':
    try:
        main ()
    except rospy.ROSInterruptException:
        pass
```


## Publish and Subscribe Turtlebot
```Python
#!/usr/bin/env python
import rospy
from geometry_msgs.msg import Twist
from nav_msgs.msg import Odometry

pos_data     = Odometry()
velocity_msg = Twist()

# เมื่อ Topic ทำงาน Publish ฟังก์ชั่นนี้จะถูกเรียก
def pos_callback(_pos_data):
	global pos_data
	pos_data = _pos_data
	#print(_pos_data)


def main ():
    rospy.init_node('listener', anonymous=True)
    pub     = rospy.Publisher('/cmd_vel', Twist, queue_size=10)
    pos_sub = rospy.Subscriber('/odom', Odometry, pos_callback) # รับตำแหน่งหุ่นยนต์จาก Odometry
    rate = rospy.Rate(10) # 10 Hz

    velocity_msg.linear.x = 0.5
    velocity_msg.linear.y = 0
    velocity_msg.linear.z = 0
    velocity_msg.angular.x = 0
    velocity_msg.angular.y = 0
    velocity_msg.angular.z = 0

    i = 0
    while not rospy.is_shutdown():
        rospy.loginfo("X: %f" % pos_data.pose.pose.position.x)
	
	if (pos_data.pose.pose.position.x > 0.5):
	    velocity_msg.linear.x = 0
	    velocity_msg.angular.z = 0
	    pub.publish(velocity_msg)

        i += 1
        # END
        rate.sleep()
        
if __name__ == '__main__':
    try:
        main ()
    except rospy.ROSInterruptException:
        pass
```


## Author  
SARUCHA YANYONG & NATTAPAT KOOMKLANG


## References
* [Creating Package](http://wiki.ros.org/ROS/Tutorials/CreatingPackage)
* [Understanding Nodes](http://wiki.ros.org/ROS/Tutorials/UnderstandingNodes)
* [Installing and Configuring Environment](http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment)
* [Teleop Node and publish topic](http://wiki.ros.org/ROS/Tutorials/UnderstandingTopics)
* [Control turtlesim using Python](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29)

