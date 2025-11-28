cmake_minimum_required(VERSION 3.20)

project(apriltag_viz)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(rclcpp REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(image_transport REQUIRED)
find_package(cv_bridge REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(apriltag_msgs REQUIRED)

add_library(apriltag_viz SHARED src/apriltag_viz.cpp)
target_link_libraries(apriltag_viz PUBLIC
  rclcpp::rclcpp
  rclcpp_components::component
  rclcpp_components::component_manager
  image_transport::image_transport
  cv_bridge::cv_bridge
  sensor_msgs::sensor_msgs_library
  ${apriltag_msgs_TARGETS}
)
rclcpp_components_register_nodes(apriltag_viz "AprilVizNode")

install(TARGETS apriltag_viz
  EXPORT export_${PROJECT_NAME}
  DESTINATION lib)

install(DIRECTORY launch DESTINATION share/${PROJECT_NAME})

ament_package()
