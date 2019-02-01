cmake_minimum_required(VERSION 2.8.3)
project(beginner_tutorial)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS 
  rospy
  std_msgs
  roscpp
  genmsg
  message_generation
 )

## Generate messages in the 'msg' folder
add_message_files(
  FILES
  Num.msg
)



## Generate added messages and services with any dependencies listed here
generate_messages(
  DEPENDENCIES
  std_msgs  # Or other packages containing msgs
)

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES pcl_downsample
  CATKIN_DEPENDS 
    roscpp
    rospy
    genmsg
    std_msgs
    message_runtime
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)
add_executable (talker src/talker.cpp)
target_link_libraries (talker ${catkin_LIBRARIES})
add_dependencies(talker beginner_tutorial_generate_messages_cpp)

add_executable (listener src/listener.cpp)
target_link_libraries (listener ${catkin_LIBRARIES})
add_dependencies(listener beginner_tutorial_generate_messages_cpp)

