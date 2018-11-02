cmake_minimum_required(VERSION 3.10.0 FATAL_ERROR)

project(test-ci CXX)

set(SAMPLE_SRC src/hello.cpp)

add_executable(${PROJECT_NAME} ${SAMPLE_SRC})
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 14)