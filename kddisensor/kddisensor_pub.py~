#!/usr/bin/env python
# -*- coding:utf-8 -*-

import rospy
from std_msgs.msg import String
from kddisensor_msgs.msg import KDDIsensor
from sensor_msgs.msg import Image
import time
from rospy_message_converter import message_converter
import json
import cv2
from cv_bridge import CvBridge, CvBridgeError

NODE_NAME = 'kddisensor_pub'
        
if __name__ == '__main__':
    rospy.init_node(NODE_NAME)
    pub_data = rospy.Publisher(NODE_NAME+"/latest_data", KDDIsensor,queue_size=1)
    pub_figure = rospy.Publisher(NODE_NAME+"/figure", Image,queue_size=1)
    jsonfile_name = "/home/a-mizutani/catkin_ws/src/kddisensor/kddisensor_latest_data.json"
    figurefile_name = "/home/a-mizutani/catkin_ws/src/kddisensor/kddifigure.png"
    interval = 100
    bridge = CvBridge()
    while not rospy.is_shutdown():
        rospy.loginfo("publish kddisensor data and figure.")
        f = open(jsonfile_name)
        jsondata = json.load(f)
        f.close()
        kddisensor_msg = message_converter.convert_dictionary_to_ros_message('kddisensor_msgs/KDDIsensor', jsondata)
        pub_data.publish(kddisensor_msg)
        figure = cv2.imread(figurefile_name)
        figure_msg = bridge.cv2_to_imgmsg(figure)
        #figure_msg.data = figure.reshape(figure_msg.height * figure_msg.step)
        pub_figure.publish(figure_msg)
        time.sleep(interval)
        
    
