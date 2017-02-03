cmake_minimum_required(VERSION 2.8.3)
project(bot_core_lcmtypes)

find_package(catkin REQUIRED COMPONENTS
lcm_catkin
)

catkin_package(
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS lcm_catkin
)

FindLCM(../../)

AddLCM(
bot_core_atlas_command_t
bot_core_force_torque_t
bot_core_gps_data_t
bot_core_gps_satellite_info_list_t
bot_core_gps_satellite_info_t
bot_core_image_metadata_t
bot_core_images_t
bot_core_image_sync_t
bot_core_image_t
bot_core_ins_t
bot_core_joint_angles_t
bot_core_joint_state_t
bot_core_kvh_raw_imu_batch_t
bot_core_kvh_raw_imu_t
bot_core_planar_lidar_t
bot_core_pointcloud2_t
bot_core_pointcloud_t
bot_core_pointfield_t
bot_core_pose_t
bot_core_position_3d_t
bot_core_quaternion_t
bot_core_raw_t
bot_core_rigid_transform_t
bot_core_robot_state_t
bot_core_robot_urdf_t
bot_core_sensor_status_t
bot_core_six_axis_force_torque_array_t
bot_core_six_axis_force_torque_t
bot_core_system_status_t
bot_core_twist_t
bot_core_utime_t
bot_core_vector_3d_t
)

AddSpyLCM(bot2 ../../java/src/bot2_spy/ImagePlugin.java ../../java/src/bot2_spy/PlanarLidarPlugin.java)

GenerateLCM()
