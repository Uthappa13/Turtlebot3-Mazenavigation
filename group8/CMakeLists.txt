cmake_minimum_required(VERSION 3.8)
project(group8)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(mage_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)
find_package(ros2_aruco_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)

include_directories(include/group8)


#Turtlebot_navigation
add_executable(Turtlebot_navigation src/navigate.cpp)
ament_target_dependencies(Turtlebot_navigation rclcpp mage_msgs geometry_msgs std_msgs tf2_ros tf2 tf2_geometry_msgs nav_msgs ros2_aruco_interfaces)
install(TARGETS Turtlebot_navigation DESTINATION lib/${PROJECT_NAME})

#Broadcaster
add_executable(broadcaster src/broadcaster.cpp)
ament_target_dependencies(broadcaster rclcpp mage_msgs geometry_msgs std_msgs tf2_ros tf2 tf2_geometry_msgs nav_msgs ros2_aruco_interfaces)
install(TARGETS broadcaster DESTINATION lib/${PROJECT_NAME})

install(DIRECTORY include config launch DESTINATION share/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()


ament_package()
