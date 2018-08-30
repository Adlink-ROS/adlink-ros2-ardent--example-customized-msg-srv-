## adlink-ros2-example-customized-msg-srv
* platform: ROS 2.0 Ardent Apalone (deb-20180328-)
* Build tool: colcon build
* DDS:   ADLINK OpenSplice 
* RMW_IMPLEMENTATION: rmw_opensplice_cpp


This example shows how to create customized msg/srv based on the ROS 2 existing examples. Several bugs and issues are corrected due to the change of build tool of ROS 2. 

### rosidl_tutorial_msgs:  include the customized messages and services to be used by rosidl_tutorial
* contact.msg
* AddTwoFloats.srv

### rosidl_tutorials:     include the programs and a customzied message
* AddressBook.msg		   ->  composed of a contact-msg-type array
* publish_address_book.cpp   ->  publish few contacts
* publish_contact.cpp        ->  publish one contact
* rv_server.cpp

## build and source:
1. cd rosidl_tutorials_msgs
2. colcon build
3. source install/setup.bash      ->   the package of rosidl_tutorials_msgs should be registered 
4. cd ..
5. cd rosidl_tutorials 
6. colcon build
7. source install/setup.bash
	    	
## run:
 __*publish a customized message*__		
1. ros2 run rosidl_tutorials publish_address_book
2. or ros2 run rosidl_tutorials publish_contact
3. ros2 topic list               -> there's a topic, /contact
4. ros2 topic echo /contact      -> to check if the message is issuing
5. or ros2 topic echo /address_book

  __*run a service server and client*__
1. ros2 run rosidl_tutorials srv_server
2. ros2 service list             -> there's a service, add_two_floats
3. ros2 run rosidl_tutorials srv_client  -> return the result of sum of the both floats
      *Result of add_two_floats: 5.000000*
4. or  ros2 service call /add_two_floats rosidl_tutorials_msgs/AddTwoFloats "{'a':1.0,'b':2.0}"
      *response:*
      *rosidl_tutorials_msgs.srv.AddTwoFloats_Response(sum=3.0)*

			

