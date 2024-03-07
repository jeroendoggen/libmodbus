cmake_minimum_required(VERSION 3.23)

project(modbus)

add_custom_command(OUTPUT config.h COMMAND cd ${CMAKE_CURRENT_LIST_DIR} &&
                                           ./autogen.sh && ./configure)

if(NOT TARGET ${PROJECT_NAME})
  add_library(${PROJECT_NAME})

  target_sources(${PROJECT_NAME} PRIVATE FILE_SET configuration TYPE HEADERS FILES config.h)
  target_sources(${PROJECT_NAME} PUBLIC FILE_SET public_headers TYPE HEADERS FILES src/modbus.h src/modbus-rtu.h src/modbus-tcp.h src/modbus-version.h)
  target_sources(${PROJECT_NAME} PRIVATE src/modbus.c src/modbus-data.c src/modbus-rtu.c src/modbus-tcp.c)
endif()
