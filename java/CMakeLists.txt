if(NOT JAVA_FOUND)
  message(STATUS "Java not found: not building Java LCM-SPY plugins")
  return()
endif()
if(NOT TARGET lcm-java)
  message(STATUS "lcm-java not found: not building Java LCM-SPY plugins")
  return()
endif()

message(STATUS "Found Java and lcm-java: building Java LCM-SPY plugins")

set(src_dir ${CMAKE_CURRENT_SOURCE_DIR}/src)
set(jar_fname lcmspy_plugins_bot2.jar)

set(java_sources
  src/bot2_spy/ImagePlugin.java
  src/bot2_spy/PlanarLidarPlugin.java
)

add_jar(lcmspy_plugins_bot2
  INCLUDE_JARS lcm-java lcmtypes_bot2-core-jar
  SOURCES ${java_sources}
)

install_jar(lcmspy_plugins_bot2 share/java)
