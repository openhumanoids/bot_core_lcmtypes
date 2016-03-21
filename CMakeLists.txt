cmake_minimum_required(VERSION 2.6.0)

set(POD_NAME bot2-core)

include(cmake/pods.cmake)

include(cmake/lcmtypes.cmake)
lcmtypes_build(C_AGGREGATE_HEADER bot_core CPP_AGGREGATE_HEADER bot_core JARNAME lcmtypes_bot2-core C_LIBNAME lcmtypes_bot2-core)

add_subdirectory(java)
