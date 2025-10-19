cmake_minimum_required(VERSION 3.0.2)
project(RFID_tag_plugin)

## Padrão do Noetic (C++14 é ok; pode ser 17 também)
add_compile_options(-std=c++14)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf2_ros
  gazebo_msgs
  geometry_msgs
  sensor_msgs
  std_msgs
)

## Gazebo Classic 11
find_package(gazebo REQUIRED)

## yaml-cpp do sistema
find_package(yaml-cpp REQUIRED)

catkin_package(
  CATKIN_DEPENDS roscpp tf2_ros gazebo_msgs geometry_msgs sensor_msgs std_msgs
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
)

link_directories(${GAZEBO_LIBRARY_DIRS})

## Biblioteca de plugin (SensorPlugin)
add_library(${PROJECT_NAME} SHARED
  src/tags.cpp
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
  ${GAZEBO_LIBRARIES}
  yaml-cpp
)

## Instala a .so no local padrão de plugins
install(TARGETS ${PROJECT_NAME}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
