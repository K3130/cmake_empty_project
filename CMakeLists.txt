cmake_minimum_required(VERSION 3.0)

project(project_test VERSION 0.1 LANGUAGES CXX)


enable_testing()

find_package(Boost REQUIRED)


aux_source_directory (src SRC_LIST)

include_directories (include)

add_executable (main ${SRC_LIST})

set (EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED on)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Werror")

set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_BUILD_TYPE Release)


set (TESTS_SOURCES ${PROJECT_SOURCE_DIR}/tests/test1.cpp)
find_package (Boost COMPONENTS unit_test_framework REQUIRED)
include_directories(${Boost_INCLUDE_DIRS})
set (TEST test_${PROJECT})
add_executable (${TEST} ${TESTS_SOURCES})
target_link_libraries (${TEST} ${PROJECT} ${Boost_LIBRARIES})
enable_testing ()
add_test (${TEST} ${TEST})
