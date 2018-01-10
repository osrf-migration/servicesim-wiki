# ROS API

### Robot interface

These are interfaces to receive sensor data and send commands to the robot.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | -----------------  | ------------
/servicebot/head_controller/command | Message | Topic to send commands to the pan-tilt head controller | [Float64MultiArray](https://github.com/ros/std_msgs/blob/groovy-devel/msg/Float64MultiArray.msg) | gazebo_ros_control | No
/servicebot/joint_states | Message | Position, velocity, torque of the various robot joints | [JointState](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/JointState.msg) | joint_state_controller | No
/servicebot/scan | Message | Lidar data | [PointCloud](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/PointCloud.msg) | gazebo_ros_block_laser | No
/servicebot/imu | Message | IMU data | [Imu](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Imu.msg) | gazebo_ros_imu | No
/servicebot/camera_front/camera_info | Message | Calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | No
/servicebot/camera_front/image_raw (or image_rect_color) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | No
/servicebot/camera_rear/camera_info | Message | Calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | No
/servicebot/camera_rear/image_raw (or image_rect_color) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | No
/servicebot/cmd_vel | Message | Velocity sent to the mobile base | [Twist](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/Twist.msg) | gazebo_ros_diff_drive | No
/servicebot/odom | Message | Odometry data of the robot | [Odometry](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Odometry.msg) | gazebo_ros_diff_drive | No
/servicebot/<JOINT_NAME>_controller/command | Message | command topic to control individual robot joints | [Float64](https://github.com/ros/std_msgs/blob/groovy-devel/msg/Float64.msg) | gazebo_ros_control | No
/servicebot/goal | Message | goal sent to navigation algorithm | [PoseStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseStamped.msg) | | No
/servicebot/pickup_guest | Service? | custom msg | | | No | 
/servicebot/dropoff_guest | Service? | custom msg | | | No | 


### Task interface

These are interfaces to interact with the flow of the task.

Topic name | Message / service | Description | Message definition | Implemented?
---------- | ----------------- | ----------- | ------------------ | -----------
/example | Message | Example description | Link to source | No