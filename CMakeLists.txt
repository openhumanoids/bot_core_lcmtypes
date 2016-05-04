project(bot2-core)
cmake_minimum_required(VERSION 2.8.12)

find_package(lcm REQUIRED)
include(${LCM_USE_FILE})

add_subdirectory(lcmtypes)
add_subdirectory(java)
