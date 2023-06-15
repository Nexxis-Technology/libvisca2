cmake_minimum_required(VERSION 3.8)
project(libvisca)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

ament_auto_add_library(${PROJECT_NAME} SHARED
  src/libvisca.cpp
)

ament_auto_add_executable(cli
  src/cli.cpp
)

ament_auto_add_executable(visca_test
  src/test.cpp
)

if(BUILD_TESTING)
  find_package(ament_cmake_cpplint REQUIRED)
  find_package(ament_cmake_lint_cmake REQUIRED)
  find_package(ament_cmake_cppcheck REQUIRED)
  ament_cpplint(MAX_LINE_LENGTH 120)
  ament_lint_cmake()
  set(ENV{AMENT_CPPCHECK_ALLOW_SLOW_VERSIONS} 1)
  ament_cppcheck()
endif()

ament_auto_package(
  # INSTALL_TO_SHARE
    # launch
    # params
)
