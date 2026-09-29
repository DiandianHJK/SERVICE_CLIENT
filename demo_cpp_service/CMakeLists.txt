cmake_minimum_required(VERSION 3.20)
project(demo_cpp_service)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(chapt4_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(turtlesim_msgs REQUIRED)
add_executable(turtle_control src/TurtleController.cpp)
target_link_libraries(turtle_control 
rclcpp::rclcpp 
geometry_msgs::geometry_msgs
turtlesim_msgs::turtlesim_msgs
chapt4_interfaces::chapt4_interfaces
)
add_executable(patrol_client src/patrol_client.cpp)
target_link_libraries(patrol_client
rclcpp::rclcpp
chapt4_interfaces::chapt4_interfaces
)

install(
  TARGETS
    turtle_control
    patrol_client
  DESTINATION lib/${PROJECT_NAME}
)
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
