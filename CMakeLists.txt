option(OPENCL_ACC "Enable OpenCL acceleration" OFF)
option(CUDA_ACC "Enable CUDA acceleration" OFF)

cmake_minimum_required(VERSION 3.10)
project(Vehicle_ROI_Timer)

set(CMAKE_CXX_STANDARD 17)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_definitions(-DDEBUG_MODE)
endif()

if (CUDA_ACC)
    message(STATUS "CUDA Acceleration: ${CUDA_ACC}")
    add_definitions(-DCUDA_ACC)
endif()

if (OPENCL_ACC)
    message(STATUS "OpenCL Acceleration: ${OPENCL_ACC}")
    add_definitions(-DOPENCL_ACC)
endif()

# Find OpenCV
find_package(OpenCV REQUIRED)

# Include directories
include_directories(${OpenCV_INCLUDE_DIRS} include)

# Source files
set(SOURCES
    src/main.cpp
    src/vehicle_roi_timer.cpp
    src/yolov11.cpp
)

# Executable
add_executable(vehicle_roi_timer ${SOURCES})

# Link OpenCV libraries
target_link_libraries(vehicle_roi_timer ${OpenCV_LIBS})
