# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
project(cob_marker)
# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS roscpp pcl pcl_ros nodelet cv_bridge opencv2 message_filters tf tf_conversions cob_object_detection_msgs visualization_msgs actionlib libzxing libdmtx-dev)

# include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})
# CATKIN_MIGRATION: removed during catkin migration
# cmake_minimum_required(VERSION 2.4.6)

# CATKIN_MIGRATION: removed during catkin migration
# include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)


# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_init()

INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/common/include ${PROJECT_SOURCE_DIR}/ros/include /usr/include/ImageMagick)
LINK_DIRECTORIES(${PROJECT_SOURCE_DIR}/libs )

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#add_message_files(
  FILES
  # TODO: List your msg files here
)
#uncomment if you have defined services
#add_service_files(
  FILES
  # TODO: List your msg files here
)

add_executable(cob_marker
	ros/src/marker_action.cpp
	common/src/MagickBitmapSource.cpp
)

target_link_libraries(cob_marker dmtx)

# rostest
rosbuild_add_roslaunch_check(ros/launch)
## Generate added messages and services with any dependencies listed here
generate_messages(
    #TODO DEPENDENCIES geometry_msgs std_msgs
)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS roscpp pcl pcl_ros nodelet cv_bridge opencv2 message_filters tf tf_conversions cob_object_detection_msgs visualization_msgs actionlib libzxing libdmtx-dev
    CATKIN_DEPENDS # TODO
    INCLUDE_DIRS # TODO include
    LIBRARIES # TODO
)