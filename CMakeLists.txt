project(bot2-core)
cmake_minimum_required(VERSION 2.8.12)

# TODO remove when minimum CMake >= 3.7
if(CMAKE_VERSION VERSION_LESS 3.7)
  list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
endif()

find_package(lcm REQUIRED)
include(${LCM_USE_FILE})

add_subdirectory(lcmtypes)
add_subdirectory(java)
add_subdirectory(pkgconfig)
