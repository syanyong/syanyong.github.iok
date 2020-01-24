# Non-Degree Mobile Robot Trainner

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
        
    while not rospy.is_shutdown():
        # TODO
        velocity_msg.linear.x = 1
        
        # END
        pub.publish(velocity_msg)
        rate.sleep()
        
if __name__ == '__main__':
    try:
        main ()
    except rospy.ROSInterruptException:
        pass
```


## 
