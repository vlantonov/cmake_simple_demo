cmake_minimum_required(VERSION 2.8.11)

project(simple_demo CXX)

if("${CMAKE_CXX_COMPILER_ID}" MATCHES "(GNU|Clang)")
    set(CMAKE_CXX_FLAGS "-std=c++11")
endif()

include(ExternalProject)

ExternalProject_Add(simple
	GIT_REPOSITORY https://github.com/oracle2025/cmake_simple_lib.git
	INSTALL_DIR ${PROJECT_BINARY_DIR}
	CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR>)

if (WIN32)
set(SIMPLE_LIBS simple.lib)
else() 
set(SIMPLE_LIBS -lsimple)
endif()

include_directories(${PROJECT_BINARY_DIR}/include)
link_directories(${PROJECT_BINARY_DIR}/lib)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

add_subdirectory(src)

