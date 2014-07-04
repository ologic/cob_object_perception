# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
project(cob_read_text)
# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS opencv2 roscpp sensor_msgs pr2_mechanism_controllers cv_bridge std_msgs image_transport cob_tesseract pcl pcl_ros geometry_msgs sensor_msgs cob_read_text_data cob_tesseract_data)

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

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# add include search paths
INCLUDE_DIRECTORIES(	${PROJECT_SOURCE_DIR}/ros/include
			${PROJECT_SOURCE_DIR}/common/include)

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

#common commands for building c++ executables and libraries
#add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#
# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_add_boost_directories()
#find_package(Boost REQUIRED COMPONENTS system thread filesystem)
include_directories(${Boost_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES})


# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_add_boost_directories()

add_library(read_text	common/src/text_detect.cpp)

add_executable(run_detect	common/src/run_detection.cpp common/src/text_detect.cpp)

add_executable(cob_read_text ros/src/cob_read_text.cpp)
target_link_libraries(cob_read_text read_text)
target_link_libraries(cob_read_text ${Boost_LIBRARIES})

add_executable(read_evaluation ros/src/read_evaluation.cpp)

add_executable(labelBox ros/src/labelBox.cpp)
target_link_libraries(labelBox ${Boost_LIBRARIES})

add_executable(create_correlation common/src/createCorrelation.cpp)
target_link_libraries(create_correlation ${Boost_LIBRARIES})

add_executable(record_kinect_prosilica ros/src/recordKinPro.cpp)
target_link_libraries(record_kinect_prosilica ${Boost_LIBRARIES})

add_executable(script_for_imglist common/src/convertXML.cpp)

add_executable(showPCD common/src/showPCD.cpp)
target_link_libraries(showPCD ${Boost_LIBRARIES})
## Generate added messages and services with any dependencies listed here
generate_messages(
    #TODO DEPENDENCIES geometry_msgs std_msgs
)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS opencv2 roscpp sensor_msgs pr2_mechanism_controllers cv_bridge std_msgs image_transport cob_tesseract pcl pcl_ros geometry_msgs sensor_msgs cob_read_text_data cob_tesseract_data
    CATKIN_DEPENDS # TODO
    INCLUDE_DIRS # TODO include
    LIBRARIES # TODO
)