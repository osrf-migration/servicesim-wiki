# ROS API

### Robot interface

These are interfaces to receive sensor data and send commands to the robot.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | -----------------  | ------------
`/servicebot/joint_states` | Message | Position, velocity, torque of the various robot joints | [JointState](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/JointState.msg) | joint_state_controller | No
`/servicebot/scan` | Message | Lidar data | [LaserScan](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/LaserScan.msg) | gazebo_ros_gpu_laser | No
`/servicebot/imu` | Message | IMU data | [Imu](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Imu.msg) | gazebo_ros_imu | No
`/servicebot/camera_front/camera_info` | Message | Calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | No
`/servicebot/camera_front/image_raw` (or image_rect_color) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | No
`/servicebot/camera_rear/camera_info` | Message | Calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | No
`/servicebot/camera_rear/image_raw` (or image_rect_color) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | No
`/servicebot/cmd_vel` | Message | Velocity sent to the mobile base | [Twist](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/Twist.msg) | gazebo_ros_diff_drive | No
`/servicebot/odom` | Message | Odometry data of the robot | [Odometry](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Odometry.msg) | gazebo_ros_diff_drive | No
`/servicebot/<JOINT_NAME>_controller/command` | Message | command topic to control individual robot joints | [Float64](https://github.com/ros/std_msgs/blob/groovy-devel/msg/Float64.msg) | gazebo_ros_control | No
`/servicebot/goal` | Message | goal sent to navigation algorithm | [PoseStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseStamped.msg) | | No


### Task interface

These are interfaces to interact with the flow of the task.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | ------------------ | -----------
`/servicesim/new_task` | Service | Start a new task and receive information about its goals (guest, pick-up location, etc) | [NewTask.srv](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/NewTask.srv) | servicesim::Competition | In progress on branch `game`
`/servicesim/pickup_guest` | Service | Service to call to get a guest to follow the robot | [PickUpGuest](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/PickUpGuest.srv) | servicesim::Competition | In progress on branch `game`
`/servicesim/dropoff_guest` | Service | Service to call to get a guest to stop following the robot | [DropOffGuest](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/DropOffGuest.srv) | servicesim::Competition | In progress on branch `game`
`/servicesim/score` | Message | Get periodic score notifications | [Score](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/msg/Score.msg) | servicesim::Competition | In progress on branch `game`