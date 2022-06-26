cmake_minimum_required(VERSION 2.8.3)
project(obstacle_detection)

# find catkin packages
find_package(catkin REQUIRED COMPONENTS pcl_conversions
                    					pcl_ros
                    					roscpp
                    					sensor_msgs
                    					dynamic_reconfigure)
find_package(Boost REQUIRED)
find_package(PCL 1.7 REQUIRED)


generate_dynamic_reconfigure_options(
  cfg/obstacle_detection.cfg
)
                    					


include_directories(BEFORE ${PCL_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})


catkin_package(CATKIN_DEPENDS dynamic_reconfigure)

s
rosbuild_add_executable(obstacle_detection src/obstacle_detection.cpp)
# make sure configure headers are built before any node using them
add_dependencies(obstacle_detection ${PROJECT_NAME}_gencfg)
target_link_libraries(obstacle_detection ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${pcl_segmentation})
