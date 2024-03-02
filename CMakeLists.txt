cmake_minimum_required(VERSION 3.0.2)
project(mocap_optitrack)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  roscpp
  geometry_msgs
  tf
)

## Your package locations should be listed before other locations
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

## Declare a C++ library
add_library(${PROJECT_NAME}
  src/mocap_datapackets.cpp
  src/mocap_config.cpp
  src/Socket.cpp
)

## Declare a C++ executable
add_executable(mocap_node src/mocap_node.cpp)

## Specify libraries to link a library or executable target against
target_link_libraries(mocap_node
  ${PROJECT_NAME}
  ${catkin_LIBRARIES}
)

## Mark executables and/or libraries for installation
install(TARGETS mocap_node ${PROJECT_NAME}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

## Mark other files for installation (e.g. launch and bag files, etc.)
install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS roscpp geometry_msgs tf
)
