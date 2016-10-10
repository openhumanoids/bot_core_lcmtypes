project(bot2-core)
cmake_minimum_required(VERSION 3.1)

include(CMakePackageConfigHelpers)

find_package(PythonInterp)
find_package(Java)

if(JAVA_FOUND)
  include(UseJava)
endif()

# TODO remove when minimum CMake >= 3.7
if(CMAKE_VERSION VERSION_LESS 3.7)
  list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
endif()

find_package(lcm REQUIRED)
include(${LCM_USE_FILE})

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_subdirectory(lcmtypes)
add_subdirectory(java)
add_subdirectory(pkgconfig)
