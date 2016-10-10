if(WIN32)
  set(CONFIG_INSTALL_DIR CMake)
else()
  set(CONFIG_INSTALL_DIR lib${LIB_SUFFIX}/${PROJECT_NAME}/cmake)
endif()

if(PYTHONINTERP_FOUND)
  set(python_args PYTHON_SOURCES python_install_sources)
endif()
if(JAVA_FOUND AND TARGET lcm-java)
  set(java_args JAVA_SOURCES java_sources)
endif()

lcm_wrap_types(
  C_SOURCES c_sources
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
  bot_core_viewer_command_t.lcm
  bot_core_viewer_draw_t.lcm
  bot_core_viewer_geometry_data_t.lcm
  bot_core_viewer_link_data_t.lcm
  bot_core_viewer_load_robot_t.lcm
)

add_library(lcmtypes_bot2-core ${c_sources})
target_include_directories(lcmtypes_bot2-core INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>)
target_link_libraries(lcmtypes_bot2-core lcm)
set_target_properties(lcmtypes_bot2-core PROPERTIES POSITION_INDEPENDENT_CODE ON)

lcm_install_headers(
  ${c_install_headers}
  ${cpp_install_headers}
  DESTINATION include/lcmtypes
)

add_library(lcmtypes_bot2-core-cpp INTERFACE)
target_include_directories(lcmtypes_bot2-core-cpp INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>)

install(TARGETS lcmtypes_bot2-core lcmtypes_bot2-core-cpp
  EXPORT ${PROJECT_NAME}Targets
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib${LIB_SUFFIX}
  ARCHIVE DESTINATION lib${LIB_SUFFIX}
  INCLUDES DESTINATION include/lcmtypes
)

if(PYTHONINTERP_FOUND)
  lcm_install_python(${python_install_sources})
endif()

if(JAVA_FOUND)
  if(NOT TARGET lcm-java)
    message(STATUS "lcm-java not found: not building Java LCM type bindings")
  else()
    add_jar(lcmtypes_bot2-core-jar
      OUTPUT_NAME lcmtypes_bot2-core
      INCLUDE_JARS lcm-java
      SOURCES ${java_sources}
    )

    install_jar(lcmtypes_bot2-core-jar share/java)

    set(BOT2-CORE_INCLUDE_JAVA
      "include(\${CMAKE_CURRENT_LIST_DIR}/bot2-coreJavaTargets.cmake)"
    )
    export_jars(
      FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}JavaTargets.cmake
      TARGETS lcmtypes_bot2-core-jar
    )
    install_jar_exports(
      FILE ${PROJECT_NAME}JavaTargets.cmake
      DESTINATION ${CONFIG_INSTALL_DIR}
      TARGETS lcmtypes_bot2-core-jar
    )
  endif()
endif()

configure_package_config_file(
  ${PROJECT_SOURCE_DIR}/${PROJECT_NAME}Config.cmake.in
  ${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
  INSTALL_DESTINATION ${CONFIG_INSTALL_DIR}
)

# Exported targets for build directory
export(
  TARGETS lcmtypes_bot2-core
  FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake
)

# Exported targets for installation
install(EXPORT ${PROJECT_NAME}Targets
  DESTINATION ${CONFIG_INSTALL_DIR}
  FILE ${PROJECT_NAME}Targets.cmake
)

# Install package configuration files
install(FILES
  ${PROJECT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
  DESTINATION ${CONFIG_INSTALL_DIR}
)
