cmake_minimum_required(VERSION 2.6.0)

set(POD_NAME bot2-core)

include(cmake/pods.cmake)

include(cmake/lcmtypes.cmake)
lcmtypes_build(C_AGGREGATE_HEADER bot_core.h CPP_AGGREGATE_HEADER bot_core.hpp)

# TODO: Get building in Win32 again
if(NOT WIN32)
  add_subdirectory(java)
endif()
