Heron position controller
=========================
Python file for controlling position of Heron using GPS and ROS topics.


The heron has a variety of topics available with different information on all of them. 
The topics can be divided into multiple categories as follows:


Command input topics
------


### /cmd_drive
**Input :**
- Left thruster : 0 - 1.0
- Right thruster : 0 - 1.0

### /cmd_helm
**Input :**
- Thrust : Newtons
- Yaw rate : rad/s


### /cmd_wrench
**Input :**
- Force vector
- Torque vector

### /cmd_course
- Absolute yaw angle : radians : Doesn't work right now.
- speed : 0 - 1.4 m/sec : Works but reliability is not confirmed.



IMU output topics
------

#### /imu/compass_heading
None

#### /imu/declination
None

#### /imu/raw_compass_heading
TBD

#### /imu/data
**Output :**
- Orientation : Quaternion
- Angular velocities : rad/sec
- Linear acceleration : m/sec^2


/imu/compass_heading = data = nan
/imu/declination = Nothing
/imu/raw_compass_heading = West is 0, North is 1.57, East is 3.14/-3.14, South is -1.57
/imu/data = Quaternion Orientation, Angular velocities, Linear acceleration  
/imu/mag = magnetometer data in x,y,z              
/imu/rpy = vector x,y,z
/imu/data_compass =  angular velocity x,y,z, linear acceleration x,y,z         
/imu/mag_calib            
/imu/temperature

In joystick, both the thrusters don't work together.

--------------------------------------------------------------------------------

 
Node [/um6_driver]

Publications: 
 * /imu/data [sensor_msgs/Imu]
 * /imu/mag [geometry_msgs/Vector3Stamped]
 * /imu/rpy [geometry_msgs/Vector3Stamped]
 * /imu/temperature [std_msgs/Float32]
 * /rosout [rosgraph_msgs/Log]

Subscriptions: None

Services: 
 * /imu/reset
 * /um6_driver/get_loggers
 * /um6_driver/set_logger_level


contacting node http://cpr-m300-0017:44418/ ...
Pid: 933
Connections:
 * topic: /rosout
    * to: /rosout
    * direction: outbound
    * transport: TCPROS
 * topic: /imu/data
    * to: /imu_compass
    * direction: outbound
    * transport: TCPROS
 * topic: /imu/mag
    * to: /imu_compass
    * direction: outbound
    * transport: TCPROS
    
--------------------------------------------------------------------------------
Node [/imu_compass]
Publications: 
 * /imu/compass_heading [std_msgs/Float32]
 * /imu/data_compass [sensor_msgs/Imu]
 * /imu/mag_calib [geometry_msgs/Vector3Stamped]
 * /imu/raw_compass_heading [std_msgs/Float32]
 * /rosout [rosgraph_msgs/Log]

Subscriptions: 
 * /imu/data [sensor_msgs/Imu]
 * /imu/declination [std_msgs/Float32]
 * /imu/mag [geometry_msgs/Vector3Stamped]
 * /tf [tf2_msgs/TFMessage]
 * /tf_static [tf2_msgs/TFMessage]

Services: 
 * /imu_compass/get_loggers
 * /imu_compass/set_logger_level


contacting node http://cpr-m300-0017:43057/ ...
Pid: 938
Connections:
 * topic: /rosout
    * to: /rosout
    * direction: outbound
    * transport: TCPROS
 * topic: /imu/data_compass
    * to: /robot_pose_ekf
    * direction: outbound
    * transport: TCPROS
 * topic: /imu/data_compass
    * to: /controller
    * direction: outbound
    * transport: TCPROS
 * topic: /tf
    * to: /base_to_basefootprint_tf (http://cpr-m300-0017:45542/)
    * direction: inbound
    * transport: TCPROS
 * topic: /tf
    * to: /robot_state_publisher (http://cpr-m300-0017:39396/)
    * direction: inbound
    * transport: TCPROS
 * topic: /tf
    * to: /navsat_to_gps_tf (http://cpr-m300-0017:34737/)
    * direction: inbound
    * transport: TCPROS
 * topic: /tf
    * to: /robot_pose_ekf (http://cpr-m300-0017:45073/)
    * direction: inbound
    * transport: TCPROS
 * topic: /tf_static
    * to: /robot_state_publisher (http://cpr-m300-0017:39396/)
    * direction: inbound
    * transport: TCPROS
 * topic: /imu/data
    * to: /um6_driver (http://cpr-m300-0017:44418/)
    * direction: inbound
    * transport: TCPROS
 * topic: /imu/mag
    * to: /um6_driver (http://cpr-m300-0017:44418/)
    * direction: inbound
    * transport: TCPROS
 * topic: /imu/declination
    * to: /imu/declination_compute (http://cpr-m300-0017:46714/)
    * direction: inbound
    * transport: TCPROS

--------------------------------------------------------------------------------
Node [/controller]
Publications: 
 * /cmd_drive [heron_msgs/Drive]
 * /eff_wrench [geometry_msgs/Wrench]
 * /rosout [rosgraph_msgs/Log]
 * /yaw_debug [geometry_msgs/Vector3]
 * /yaw_rate_debug [geometry_msgs/Vector3]

Subscriptions: 
 * /cmd_course [unknown type]
 * /cmd_helm [unknown type]
 * /cmd_wrench [unknown type]
 * /imu/data_compass [sensor_msgs/Imu]

Services: 
 * /controller/get_loggers
 * /controller/set_logger_level


contacting node http://cpr-m300-0017:39290/ ...
Pid: 1000
Connections:
 * topic: /rosout
    * to: /rosout
    * direction: outbound
    * transport: TCPROS
 * topic: /cmd_drive
    * to: /rosserial_server
    * direction: outbound
    * transport: TCPROS
 * topic: /imu/data_compass
    * to: /imu_compass (http://cpr-m300-0017:43057/)
    * direction: inbound
    * transport: TCPROS


/axis/axis_ptz/parameter_descriptions = 
/axis/axis_ptz/parameter_updates
/axis/camera_info
/axis/cmd
/axis/image_raw/compressed
/axis/mirror
/axis/state
/axis_ptz/axis_ptz/parameter_descriptions
/axis_ptz/axis_ptz/parameter_updates
/axis_ptz/camera_info
/axis_ptz/cmd
/axis_ptz/image_raw/compressed
/axis_ptz/mirror
/axis_ptz/state
/cmd_course
/cmd_drive
/cmd_helm
/cmd_wrench
/disable_lights

/eff_wrench
    Type: geometry_msgs/Wrench

    Publishers: 
    * /controller (http://cpr-m300-0017:39657/)

    Subscribers: None

/has_wifi
/imu/compass_heading

---
data: nan

___
/imu/data

---
header: 
  seq: 16392
  stamp: 
    secs: 1558135784
    nsecs: 266663730
  frame_id: "imu_link"
orientation: 
  x: -0.891600608
  y: -0.44982862
  z: -0.036254844
  w: -0.0371276458
orientation_covariance: [0.125362828373909, -0.061878979206085205, -0.004873218480497599, -0.06187904253602028, 0.033632367849349976, 0.002453948836773634, -0.004873218480497599, 0.002453948836773634, 0.0026679513975977898]
angular_velocity: 
  x: 0.00639159119768
  y: 0.00639159119768
  z: 0.00106526519961
angular_velocity_covariance: [2.5e-05, 0.0, 0.0, 0.0, 2.5e-05, 0.0, 0.0, 0.0, 2.5e-05]
linear_acceleration: 
  x: 0.04850253
  y: 1.12813292
  z: -10.04541288
linear_acceleration_covariance: [0.0036, 0.0, 0.0, 0.0, 0.0036, 0.0, 0.0, 0.0, 0.0036]


/imu/data_compass

^Cheader: 
  seq: 27657
  stamp: 
    secs: 1558136353
    nsecs: 164558407
  frame_id: "imu_link"
orientation: 
  x: nan
  y: nan
  z: nan
  w: nan
orientation_covariance: [0.1328904628753662, 0.041348427534103394, -0.006661889608949423, 0.04134823754429817, 0.015576616860926151, -0.0021118316799402237, -0.006661814637482166, -0.002111810492351651, 0.0028081804048269987]
angular_velocity: 
  x: 0.00213053039923
  y: 0.00639159119768
  z: 0.00213053039923
angular_velocity_covariance: [2.5e-05, 0.0, 0.0, 0.0, 2.5e-05, 0.0, 0.0, 0.0, 2.5e-05]
linear_acceleration: 
  x: -0.08802311
  y: 1.11915097
  z: -10.00768869
linear_acceleration_covariance: [0.0036, 0.0, 0.0, 0.0, 0.0036, 0.0, 0.0, 0.0, 0.0036]
---



/imu/declination = None
/imu/mag

---
header: 
  seq: 33068
  stamp: 
    secs: 1558136626
    nsecs: 156127189
  frame_id: "imu_link"
vector: 
  x: 0.113830648
  y: 0.669250968
  z: 1.132813312
---

/imu/mag_calib



/imu/raw_compass_heading

data: 2.69622063637 = Changes on reset maybe? 


/imu/rpy

header: 
  seq: 4002
  stamp: 
    secs: 1558136167
    nsecs: 368932864
  frame_id: "imu_link"
vector: 
  x: 0.094339576945
  y: -3.11761622266
  z: 2.76786949838

Integrates on Z and drifts a lot.


/imu/temperature

---
data: 18.7321224213
---

/joint_states
/joy
/lights
/motor_enable
/navsat/enu

---
header: 
  seq: 12583
  stamp: 
    secs: 1558137476
    nsecs: 720462865
  frame_id: "map"
child_frame_id: "navsat"
pose: 
  pose: 
    position: 
      x: nan
      y: nan
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  covariance: [0.039605, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.039605, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.15842, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1000000.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1000000.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1000000.0]
twist: 
  twist: 
    linear: 
      x: 0.0
      y: 0.0
      z: 0.0
    angular: 
      x: 0.0
      y: 0.0
      z: 0.0
  covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
---
^Ca

/navsat/enu_datum = Nothing
/navsat/fix

---
header: 
  seq: 12920
  stamp: 
    secs: 1558137543
    nsecs: 913934989
  frame_id: "navsat"
status: 
  status: 0
  service: 1
latitude: 39.9411411667
longitude: -75.1995515
altitude: -19.2
position_covariance: [1.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 4.0]
position_covariance_type: 1
---

/navsat/nmea_sentence

---
header: 
  seq: 117417
  stamp: 
    secs: 1558137571
    nsecs: 922666795
  frame_id: "navsat"
sentence: "$GPGSA,A,3,19,29,06,05,09,25,12,23,02,,,,1.93,1.08,1.60*09"
---
/navsat/nmea_sentence_out = Nothing
/navsat/time_reference = 
---
header: 
  seq: 65
  stamp: 
    secs: 1558137638
    nsecs: 528586921
  frame_id: "navsat"
time_ref: 
  secs: 1558223507
  nsecs:         0
source: "navsat"
---
/navsat/upgrade/fix
/navsat/upgrade/nmea_sentence
/navsat/upgrade/time_reference
/navsat/upgrade/vel
/navsat/vel
---
header: 
  seq: 124
  stamp: 
    secs: 1558137731
    nsecs: 519574429
  frame_id: "navsat"
twist: 
  linear: 
    x: -0.00471782912576
    y: 0.0173764817844
    z: 0.0
  angular: 
    x: 0.0
    y: 0.0
    z: 0.0
---
/novatel/fix = Box gps coordinates
/novatel/nmea_sentence
/novatel/nmea_sentence_out
/novatel/time_reference
/novatel/vel
/reverse_time_ms
/robot_pose_ekf/odom = Doesn't publish anything.
/rosout
/rosout_agg


/sense

---
^Cheader: 
  seq: 0
  stamp: 
    secs: 1558137306
    nsecs: 721315248
  frame_id: ''
battery: 16.2778491974
current_left: 0.0
current_right: 0.0
rc: 0
rc_throttle: 0
rc_rotation: 0
rc_enable: 0
---
/status

---
header: 
  seq: 0
  stamp: 
    secs: 1558137379
    nsecs: 811380195
  frame_id: ''
hardware_id: ''
mcu_uptime: 
  secs: 2478
  nsecs:         0
connection_uptime: 
  secs: 2428
  nsecs:         0
pcb_temperature: 37.4632072449
user_current: 0.0178504828364
user_power_consumed: 9.27973747253
motor_power_consumed: 1.96030080318
total_power_consumed: 11.2400379181
---

/tf
/tf_static
/yaw_debug = Nothing
/yaw_rate_debug = Nothing



2019-05-17-20-45-54.bag = Going in a rectangle/square in the perch parking lot between 176 and 197.
2019-05-17-20-50-00.bag = Standing in the parking lot mentioned above for a long time to check the accuracy of the localization or position.