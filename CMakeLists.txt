cmake_minimum_required(VERSION 3.0.2)
project(mocap_optitrack)

# Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf
  geometry_msgs
  # 他に依存するパッケージがあればここに追加
)

# Declare a catkin package
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS roscpp tf geometry_msgs
  # 他に依存するパッケージがあればここに追加
)

# Specify additional locations of header files
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

# Declare the executable, along with its source files
# add_executable(mocap_node src/mocap_config.cpp src/mocap_node.cpp src/mocap_datapackets.cpp src/Socket.cpp)

## Declare a C++ library
add_library(${PROJECT_NAME}
  src/mocap_datapackets.cpp
  src/mocap_config.cpp
  src/Socket.cpp
)

## Declare a C++ executable
add_executable(mocap_node src/mocap_node.cpp)


# Specify libraries to link a library or executable target against
target_link_libraries(mocap_node
  ${catkin_LIBRARIES}
)

# Install targets (optional)
install(TARGETS mocap_node
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
