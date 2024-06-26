cmake_minimum_required(VERSION 3.4.1)

project(SAMPLE_APP VERSION 1.0)

set(CMAKE_EXPORT_COMPILE_COMMANDS YES)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage -std=c++17")

# Set up project variable if not defined
if (NOT DEFINED LIB_NAME OR NOT DEFINED APP_NAME OR NOT DEFINED BUILD_TARGET)
    set(APP_NAME SAMPLE_APP)
    set(SAMPLE_APP_DIFFERENT_BUILD SAMPLE_APP_X)
    set(BUILD_TARGET ${CMAKE_SYSTEM_PROCESSOR})
endif()

# Set up directory variables
set(LIBS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/libs/${BUILD_TARGET})
message(STATUS "LIBS_DIR: ${LIBS_DIR}")
set(INCLUDE_DIR ${LIBS_DIR}/include)
message(STATUS "INCLUDE_DIR: ${INCLUDE_DIR}")
set(SO_LIB_DIR ${LIBS_DIR}/lib)
set(SRC_DIR ${CMAKE_SOURCE_DIR}/src)

## Setup include directory
set(EXTERNAL_INCLUDE_DIR ${INCLUDE_DIR}/external)

## Setup output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/bin)

## Setup include directory
set(EXTERNAL_INCLUDE_DIR ${INCLUDE_DIR}/external)

## Setup application include directory

set(APPLICATION_INCLUDE_DIR ${SRC_DIR}/application)

# set sub directory of external
# set(OPENCV_INCLUDE_DIR ${EXTERNAL_INCLUDE_DIR}/opencv4)

# Include headers and sources
include_directories(
    ${SRC_DIR}
    # ${OPENCV_INCLUDE_DIR}
    ${EXTERNAL_INCLUDE_DIR}
    ${APPLICATION_INCLUDE_DIR}
)

# Include pre-compiled libraries from the install folder
file(GLOB_RECURSE EXTERNAL_LIB_FILES "${SO_LIB_DIR}/*.so*")

add_subdirectory(${SRC_DIR})
