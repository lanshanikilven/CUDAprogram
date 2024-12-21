cmake_minimum_required(VERSION 3.20)
project(global_memory  LANGUAGES CXX CUDA)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CUDA_STANDARD 14) #用于指定CUDA编译器应该使用的CUDA C++标准版本
set(CMAKE_CUDA_STANDARD_REQUIRED ON) #表明如果找不到指定版本的CUDA编译器，将报错
 set(CMAKE_CXX_STANDARD 14) #用于指定C++编译器应该使用的C++标准版本
set(CMAKE_CXX_STANDARD_REQUIRED ON) #表明如果找不到指定版本的C++编译器，将报错
#set(CMAKE_CUDA_FLAGS = "-G -g -O0")
#set(CMAKE_CUDA_FLAGS_DEBUG = "-G -g -O0")
find_package(CUDA REQUIRED)
if (CUDA_FOUND)
  messgae(STATUS "CUDA_INCLUDE_DIRS: ${CUDA_INCLUDE_DIRS}")
  messgae(STATUS "CUDA_LIBRARIES: ${CUDA_LIBRARIES}")  
  messgae(STATUS "CUDA_LIBRARY_DIRS: ${CUDA_LIBRARY_DIRS}")
else()
message(FATAL_ERROR "Cannot find CUDA")
endif()
add_executable(global_memory  global_memory.cu  common.cuh)
target_include_directories(global_memory PRIVATE ${CUDA_INCLUDE_DIRS})
target_link_libraries(global_memory PRIVATE ${CUDA_LIBRARIES})
