find_package(PythonInterp)
find_package(Java)

if(PYTHONINTERP_FOUND)
  set(python_args PYTHON_SOURCES python_install_sources)
endif()
if(JAVA_FOUND)
  set(java_args JAVA_SOURCES java_sources)
endif()

lcm_wrap_types(
  C_SOURCES sources
  C_HEADERS c_install_headers
  CPP_HEADERS cpp_install_headers
  CREATE_C_AGGREGATE_HEADER
  CREATE_CPP_AGGREGATE_HEADER
  ${python_args}
  ${java_args}
  bot_core_atlas_command_t.lcm
  bot_core_force_torque_t.lcm
  bot_core_gps_data_t.lcm
  bot_core_gps_satellite_info_list_t.lcm
  bot_core_gps_satellite_info_t.lcm
  bot_core_image_metadata_t.lcm
  bot_core_images_t.lcm
  bot_core_image_sync_t.lcm
  bot_core_image_t.lcm
  bot_core_ins_t.lcm
  bot_core_joint_angles_t.lcm
  bot_core_joint_state_t.lcm
  bot_core_kvh_raw_imu_batch_t.lcm
  bot_core_kvh_raw_imu_t.lcm
  bot_core_planar_lidar_t.lcm
  bot_core_pointcloud2_t.lcm
  bot_core_pointcloud_t.lcm
  bot_core_pointfield_t.lcm
  bot_core_pose_t.lcm
  bot_core_position_3d_t.lcm
  bot_core_quaternion_t.lcm
  bot_core_raw_t.lcm
  bot_core_rigid_transform_t.lcm
  bot_core_robot_state_t.lcm
  bot_core_robot_urdf_t.lcm
  bot_core_sensor_status_t.lcm
  bot_core_six_axis_force_torque_array_t.lcm
  bot_core_six_axis_force_torque_t.lcm
  bot_core_system_status_t.lcm
  bot_core_twist_t.lcm
  bot_core_utime_t.lcm
  bot_core_vector_3d_t.lcm
)

add_library(lcmtypes_bot2-core ${sources})
target_link_libraries(lcmtypes_bot2-core lcm)

install(FILES ${c_install_headers} DESTINATION include/lcmtypes)
install(FILES ${cpp_install_headers} DESTINATION include/lcmtypes/bot_core)

if(PYTHONINTERP_FOUND)
  lcm_install_python(${python_install_sources})
endif()

if(JAVA_FOUND)
  include(UseJava)

  add_jar(lcmtypes_bot2-core-jar
    OUTPUT_NAME lcmtypes_bot2-core
    INCLUDE_JARS lcm-java
    SOURCES ${java_sources}
  )

  install_jar(lcmtypes_bot2-core-jar share/java)
endif()
