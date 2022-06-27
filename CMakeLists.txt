cmake_minimum_required(VERSION 3.0)
project(project_test VERSION 0.1 LANGUAGES CXX)
set(PROJECT_NAME "project_test")

aux_source_directory (src SRC_LIST)
include_directories (include)
add_executable (${PROJECT_NAME} main.cpp)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/build)
set (EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED on)

if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pedantic -Wall -Wextra -Wall -Werror")
endif(CMAKE_COMPILER_IS_GNUCXX)


#GOOGLE TEST
enable_testing()

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
enable_testing()
add_executable(
  hello_test
  tests/test1.cc
)
target_link_libraries(
  hello_test
  gtest_main
)
include(GoogleTest)
gtest_discover_tests(hello_test)

#cpack
#install: sudo dpkg -i DEB_PACKAGE
#remove: sudo dpkg -r PACKAGE_NAME
install(TARGETS main)
SET(CPACK_GENERATOR "DEB")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "KK")
INCLUDE(CPack)



