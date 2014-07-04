# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
project(cob_object_categorization)
# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS roscpp opencv2 cv_bridge pcl_ros sensor_msgs message_filters image_transport cob_perception_msgs)

# include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})
# CATKIN_MIGRATION: removed during catkin migration
# cmake_minimum_required(VERSION 2.6)

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

# add include search paths
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/ros/include
		    ${PROJECT_SOURCE_DIR}/common/include)
		    #/usr/include/pcl-1.4/
		    #/usr/include/eigen3/
		    #/usr/include/boost/
		    #/usr/include/flann/
		    #/usr/include/vtk-5.4/)

# external pcl
#find_package(PCL 1.4 REQUIRED)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

# Check for sse support

# CATKIN_MIGRATION
# Find other way to find SSE
# rosbuild_check_for_sse()
#set(SSE_FLAGS "-msse2 -mfpmath=sse")


# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_add_boost_directories()

add_executable(object_categorization
				common/src/AbstractBlobDetector.cpp
				common/src/BlobFeature.cpp
				common/src/BlobList.cpp
				common/src/DetectorCore.cpp
				common/src/ICP.cpp
				common/src/JBKUtils.cpp
				common/src/Math3d.cpp
				common/src/ObjectClassifier.cpp
				#common/src/ObjectClassifierMain.cpp
				ros/src/object_categorization.cpp
				common/src/OpenCVUtils.cpp
				common/src/SharedImageJBK.cpp
				common/src/SharedImageSequence.cpp
				common/src/ThreeDUtils.cpp
				common/src/timer.cpp)
				#common/src/pcl/gfpfh.cpp)
				
add_executable(object_segmentation ros/src/segmentation_node.cpp)


# CATKIN_MIGRATION
# use link_directories() include_directories(), add_definitions(), target_link_libraries() or set_target_properties
# rosbuild_add_compile_flags(object_categorization -D__LINUX__)

# CATKIN_MIGRATION
# use link_directories() include_directories(), add_definitions(), target_link_libraries() or set_target_properties
# rosbuild_add_compile_flags(object_segmentation -D__LINUX__)

find_package(Boost REQUIRED COMPONENTS system thread filesystem)
include_directories(${Boost_INCLUDE_DIRS})
target_link_libraries(object_categorization ${Boost_LIBRARIES})
target_link_libraries(object_segmentation ${Boost_LIBRARIES})

target_link_libraries(object_categorization ${PCL_COMMON_LIBRARIES} ${PCL_IO_LIBRARIES} ${PCL_FEATURES_LIBRARIES})
target_link_libraries(object_segmentation ${PCL_COMMON_LIBRARIES} ${PCL_IO_LIBRARIES} ${PCL_FEATURES_LIBRARIES})
#target_link_libraries(object_categorization pcl_features pcl_common pcl_kdtree pcl_search pcl_filters pcl_io)
#target_link_libraries(object_segmentation pcl_features pcl_common pcl_kdtree pcl_search pcl_filters pcl_io)

#common commands for building c++ executables and libraries
#add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#
# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_add_boost_directories()
#target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES})
#add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})
## Generate added messages and services with any dependencies listed here
generate_messages(
    #TODO DEPENDENCIES geometry_msgs std_msgs
)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS roscpp opencv2 cv_bridge pcl_ros sensor_msgs message_filters image_transport cob_perception_msgs
    CATKIN_DEPENDS # TODO
    INCLUDE_DIRS # TODO include
    LIBRARIES # TODO
)