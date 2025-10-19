cmake_minimum_required(VERSION 3.0.2)
project(RFID_antenna_plugin)

add_compile_options(-std=c++14)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf   # seu código usa tf1 (TransformListener); pode migrar pra tf2 depois
  gazebo_msgs
  geometry_msgs
  sensor_msgs
  std_msgs
)

find_package(gazebo REQUIRED)
find_package(yaml-cpp REQUIRED)

catkin_package(
  CATKIN_DEPENDS roscpp tf gazebo_msgs geometry_msgs sensor_msgs std_msgs
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
)

link_directories(${GAZEBO_LIBRARY_DIRS})

add_library(${PROJECT_NAME} SHARED
  src/antenna.cpp
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
  ${GAZEBO_LIBRARIES}
  yaml-cpp
)

install(TARGETS ${PROJECT_NAME}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
