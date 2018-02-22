# ROS API

### Robot interface

These are interfaces to receive sensor data and send commands to the robot.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | -----------------  | ------------
`/servicebot/joint_states` | Message | Position, velocity, torque of the various robot joints | [JointState](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/JointState.msg) | joint_state_controller | Yes
`/servicebot/scan` | Message | Lidar data | [LaserScan](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/LaserScan.msg) | gazebo_ros_gpu_laser | Yes
`/servicebot/imu` | Message | IMU data | [Imu](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Imu.msg) | gazebo_ros_imu | Yes
`/servicebot/camera_front/camera_info` | Message | Calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | Yes
`/servicebot/camera_front/image_raw` (or image_rect_color) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | Yes
`/servicebot/camera_rear/camera_info` | Message | Calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | Yes
`/servicebot/camera_rear/image_raw` (or image_rect_color) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | Yes
`/servicebot/cmd_vel` | Message | Velocity sent to the mobile base | [Twist](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/Twist.msg) | gazebo_ros_diff_drive | Yes
`/servicebot/odom` | Message | Odometry data of the robot | [Odometry](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Odometry.msg) | gazebo_ros_diff_drive | Yes
`/servicebot/<JOINT_NAME>_controller/command` | Message | command topic to control individual robot joints | [Float64](https://github.com/ros/std_msgs/blob/groovy-devel/msg/Float64.msg) | gazebo_ros_control | Yes
`/servicebot/goal` | Message | goal sent to navigation algorithm | [PoseStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseStamped.msg) | | No
`/servicebot/rfid` | Message | RFID sensor readings | [ActorNames](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/msg/ActorNames.msg) | servicesim::VicinityPlugin | Yes

### Task interface

These are interfaces to interact with the flow of the task.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | ------------------ | -----------
`/servicesim/new_task` | Service | Start a new task and receive information about its goals (guest, pick-up location, etc) | [NewTask.srv](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/NewTask.srv) | servicesim::Competition | Yes
`/servicesim/pickup_guest` | Service | Service to call to get a guest to follow the robot | [PickUpGuest](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/PickUpGuest.srv) | servicesim::Competition | Yes
`/servicesim/dropoff_guest` | Service | Service to call to get a guest to stop following the robot | [DropOffGuest](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/DropOffGuest.srv) | servicesim::Competition | Yes
`/servicesim/score` | Message | Get periodic score notifications | [Score](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/msg/Score.msg) | servicesim::Competition | Yes
`/servicesim/room_info` | Service | Get information about a given room, such as its position in the world | [RoomInfo](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/RoomInfo.srv) | servicesim::Competition | Yes