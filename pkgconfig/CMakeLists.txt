file(TO_CMAKE_PATH "${CMAKE_INSTALL_PREFIX}" BOT2_CORE_INSTALL_PREFIX)

configure_file(lcmtypes_bot2-core.pc.in
  ${bot2-core_BINARY_DIR}/lcmtypes_bot2-core.pc @ONLY)
install(FILES ${bot2-core_BINARY_DIR}/lcmtypes_bot2-core.pc
  DESTINATION lib${LIB_SUFFIX}/pkgconfig)

if(TARGET lcmtypes_bot2-core)
  configure_file(lcmtypes_bot2-core-java.pc.in
    ${bot2-core_BINARY_DIR}/lcmtypes_bot2-core-java.pc @ONLY)
  install(FILES ${bot2-core_BINARY_DIR}/lcmtypes_bot2-core-java.pc
    DESTINATION lib${LIB_SUFFIX}/pkgconfig)
endif()
