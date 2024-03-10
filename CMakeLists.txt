cmake_minimum_required(VERSION 3.8)
project(microbot_bringup)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic -Werror)
endif()


# find dependencies
find_package(geometry_msgs REQUIRED)
find_package(joy REQUIRED)
find_package(teleop_twist_joy REQUIRED)

# list dependencies
set(dependencies
  geometry_msgs
  joy
  teleop_twist_joy
)

# install config files
install(
  DIRECTORY config
  DESTINATION share/${PROJECT_NAME}
)

# install launch files
install(
  DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)

ament_package()