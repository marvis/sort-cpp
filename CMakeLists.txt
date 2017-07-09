cmake_minimum_required(VERSION 3.5)
project(SORT_CPP)

if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
    #set(CMAKE_BUILD_TYPE "Debug")
    message(STATUS "No build type selected, default to ${CMAKE_BUILD_TYPE}")
endif()

#=== common packages ===
find_package(Boost COMPONENTS system filesystem regex REQUIRED)

#set(OpenCV_DIR ~/nfs/Robot_Tracking/opencv_root/opencv/release)
find_package( OpenCV REQUIRED )
message("Open CV version is ${OpenCV_VERSION}")

# sort_cpp
set(CMAKE_CXX_FLAGS "-std=c++0x")
add_executable(sort_cpp sort-c++/Hungarian.cpp sort-c++/KalmanTracker.cpp sort-c++/main.cpp)
target_include_directories(sort_cpp PUBLIC ./sort-c++)
target_link_libraries(sort_cpp ${OpenCV_LIBS})
