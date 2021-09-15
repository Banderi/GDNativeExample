cmake_minimum_required(VERSION 3.17)
project(GodotNeuralNetworkTests2)

set(CMAKE_CXX_STANDARD 14)
include_directories(${PROJECT_SOURCE_DIR}/godot-headers)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ../project/gdnative/windows)

add_library(simple SHARED src/simple.c)