# ROS API

### Robot interface

These are interfaces to receive sensor data and send commands to the robot.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | -----------------  | ------------
`/servicebot/joint_states` | Message | Listen to updated position, velocity, torque of the various robot joints | [JointState](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/JointState.msg) | joint_state_controller | Yes
`/servicebot/scan` | Message | Listen to lidar data | [LaserScan](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/LaserScan.msg) | gazebo_ros_gpu_laser | Yes
`/servicebot/imu` | Message | Listen to IMU data | [Imu](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Imu.msg) | gazebo_ros_imu | Yes
`/servicebot/camera_front/camera_info` | Message | Get the calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | Yes
`/servicebot/camera_front/image_raw` (or `image_rect_color`) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | Yes
`/servicebot/camera_rear/camera_info` | Message | Get the calibration and resolution of the camera | [CameraInfo](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/CameraInfo.msg) | gazebo_ros_camera | Yes
`/servicebot/camera_rear/image_raw` (or `image_rect_color`) | Message | Image sent by the camera | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | gazebo_ros_camera | Yes
`/servicebot/cmd_vel` | Message | Send velocities to the mobile base | [Twist](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/Twist.msg) | gazebo_ros_diff_drive | Yes
`/servicebot/odom` | Message | Get odometry data from the robot | [Odometry](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Odometry.msg) | gazebo_ros_diff_drive | Yes
`/servicebot/<JOINT_NAME>_controller/command` | Message | Send commands to control individual robot joints | [Float64](https://github.com/ros/std_msgs/blob/groovy-devel/msg/Float64.msg) | gazebo_ros_control | Yes
`/servicebot/rfid` | Message | Get RFID sensor readings | [ActorNames](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/msg/ActorNames.msg) | servicesim::VicinityPlugin | Yes

### Task interface

These are interfaces to interact with the flow of the task.

Topic name | Message / service | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | ------------------ | -----------
`/servicesim/new_task` | Service | Start a new task and receive information about its goals (guest, pick-up location, etc) | [NewTask](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/NewTask.srv) | servicesim::Competition | Yes
`/servicesim/pickup_guest` | Service | Service to call to get a guest to follow the robot | [PickUpGuest](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/PickUpGuest.srv) | servicesim::Competition | Yes
`/servicesim/dropoff_guest` | Service | Service to call to get a guest to stop following the robot | [DropOffGuest](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/DropOffGuest.srv) | servicesim::Competition | Yes
`/servicesim/score` | Message | Get periodic score notifications | [Score](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/msg/Score.msg) | servicesim::Competition | Yes
`/servicesim/room_info` | Service | Get information about a given room, such as its position in the world | [RoomInfo](https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/srv/RoomInfo.srv) | servicesim::Competition | Yes

### Example Solution interface
Interface name | Topic / Service / Action | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | ------------------ | -----------
`/servicebot/move_base_simple/goal` | Topic | Goal sent to navigation algorithm | [PoseStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseStamped.msg) | | Yes
`/servicebot/initialpose` | Topic | Initialize the localization to a given pose | [PoseWithCovarianceStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseWithCovarianceStamped.msg) | | Yes
`/servicebot/move_base/TrajectoryPlannerROS/cost_cloud` | Topic | Cost grid used for planning | [PointCloud2](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/PointCloud2.msg) | | Yes
`/servicebot/move_base/TrajectoryPlannerROS/global_plan` | Topic | Portion of the global plan that the local planner is currently attempting to follow. | [Path](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Path.msg) | | Yes
`/servicebot/move_base/TrajectoryPlannerROS/local_plan` | Topic | Local plan or trajectory that scored the highest on the last cycle. | [Path](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/Path.msg) | | Yes
`/servicebot/move_base/global_costmap/costmap` | Topic | Cost map used by the global planner | [OccupancyGrid](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/OccupancyGrid.msg) | | Yes
`/servicebot/move_base/local_costmap/costmap` | Topic | Cost map used by the local planner | [OccupancyGrid](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/OccupancyGrid.msg) | | Yes
`/servicebot/map` | Topic | Static map of the environment | [OccupancyGrid](https://github.com/ros/common_msgs/blob/jade-devel/nav_msgs/msg/OccupancyGrid.msg) | | Yes
`/servicebot/move_base/local_costmap/footprint` | Topic | Polygon representing the footrpint of the robot | [PolygonStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PolygonStamped.msg) | | Yes
`/servicebot/move_base/current_goal` | Topic | Current navigation goal | [PoseStamped](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseStamped.msg) | | Yes
`/servicebot/particlecloud` | Topic | The set of pose estimates being maintained by the particle filter | [PoseArray](https://github.com/ros/common_msgs/blob/jade-devel/geometry_msgs/msg/PoseArray.msg) | | Yes
`/servicebot/move_base/clear_costmaps` | Service | Clear all the costmaps | [Empty](https://github.com/ros/ros_comm_msgs/blob/indigo-devel/std_srvs/srv/Empty.srv) | | Yes
`/servicebot/move_base` | Action | Action to process goals | [MoveBase](https://github.com/ros-planning/navigation_msgs/blob/jade-devel/move_base_msgs/action/MoveBase.action) | | Yes

### Image demo example

Interface name | Topic / Service / Action | Description | Message definition | Gazebo plugin used | Implemented?
---------- | ----------------- | ----------- | ------------------ | ------------------ | -----------
`/servicebot/camera_front/segmented_image` | Message | Image after application of a color mask | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | `/servicebot/camera_front/segmented_image` | Message | Image after application of a color mask | [Image](https://github.com/ros/common_msgs/blob/jade-devel/sensor_msgs/msg/Image.msg) | | Yes
 | Yes