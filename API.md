# ROS API

### Robot interface

These are interfaces to receive sensor data and send commands to the robot.

Topic name | Message / service | Description | Message definition | Implemented? | Gazebo plugin used
---------- | ----------------- | ----------- | ------------------ | -----------  | ------------------
/servicebot/joint_states | Message | Position, velocity, torque of the various robot joints | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/JointState.msg | No | joint_state_controller
/servicebot/scan | Message | Lidar data | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/PointCloud.msg | No | gazebo_ros_block_laser
/servicebot/imu | Message | IMU data | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Imu.msg | No | gazebo_ros_imu
/servicebot/camera_front/camera_info | Message | Calibration and resolution of the camera | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg | No | gazebo_ros_camera
/servicebot/camera_front/image_raw (or image_rect_color) | Message | Image sent by the camera | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg | No | gazebo_ros_camera
/servicebot/camera_rear/camera_info | Message | Calibration and resolution of the camera | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg | No | gazebo_ros_camera
/servicebot/camera_rear/image_raw (or image_rect_color) | Message | Image sent by the camera | https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg | No | gazebo_ros_camera
/servicebot/cmd_vel | Message | Velocity sent to the mobile base | https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/Twist.msg | No | gazebo_ros_diff_drive
/servicebot/odom | Message | Odometry data of the robot | https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Odometry.msg | No | gazebo_ros_diff_drive
/servicebot/<JOINT_NAME>_controller/command | Message | command topic to control individual robot joints | https://github.com/ros/std_msgs/blob/groovy-devel/msg/Float64.msg | No | gazebo_ros_control
/servicebot/goal | Message | goal sent to navigation algorithm | https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseStamped.msg | No |


### Task interface

These are interfaces to interact with the flow of the task.

Topic name | Message / service | Description | Message definition | Implemented?
---------- | ----------------- | ----------- | ------------------ | -----------
/pickup_guest | Service | Service to call to get a guest to follow the robot | custom_msg | No | 
/dropoff_guest | Service | Service to call to get a guest to stop following the robot | custom_msg | No | 
/request_guest | Service | Service to call to get infromation aboutthe guest to pick up | custom_msg | No | 
