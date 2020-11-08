# cmake_minimum_required(VERSION <specify CMake version here>)
cmake_minimum_required(VERSION 3.16)

project(labs_cmake)

set(CMAKE_CXX_STANDARD 14)
SET(CMAKE_MODULE_PATH cmake)

#设置可执行文件的输出目录
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

# 利用pkg-config寻找包
# pkg-config --cflags gtk+-3.0
# pkg-config --libs gtk+-3.0
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK3 REQUIRED gtk+-3.0)

# gtk+-3.0
include_directories(${GTK3_INCLUDE_DIRS})
link_directories(${GTK3_LIBRARY_DIRS})
add_definitions(${GTK3_CFLAGS_OTHER})

add_subdirectory(labs_cmake_subdirectory)

add_executable(labs_cmake main.cpp)

target_link_libraries(labs_cmake labs_cmake_subdirectory)
target_link_libraries (labs_cmake ${GTK3_LIBRARIES})

MESSAGE(CMAKE_CXX_FLAGS_RELEASE)

IF(WIN32)
    MESSAGE(STATUS “This is Windows.”)
ELSEIF(UNIX)
    MESSAGE(STATUS “This is Linux.”)
ELSEIF(APPLE)
    MESSAGE(STATUS “This is APPLE.”)
ENDIF(WIN32)