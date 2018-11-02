cmake_minimum_required(VERSION 3.9.0 FATAL_ERROR)

project(hello-ci CXX)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

file(GLOB_RECURSE  SOURCE_LIBS ./src/hello.cpp)
file(GLOB_RECURSE  HEADER_LIBS ./src/hello.h)
add_library(${PROJECT_NAME} STATIC ${HEADER_LIBS} ${SOURCE_LIBS})
set_target_properties(hello-ci PROPERTIES LINKER_LANGUAGE CXX)
#target_link_libraries(${PROJECT_NAME} ${CONAN_LIBS})

set(SAMPLE_SRC src/main.cpp)

add_executable(${PROJECT_NAME}-run ${SAMPLE_SRC})
target_link_libraries(${PROJECT_NAME}-run ${PROJECT_NAME})
set_property(TARGET ${PROJECT_NAME}-run PROPERTY CXX_STANDARD 14)

file(GLOB_RECURSE SOURCE_LIST ./tests/test-hello.cpp)
add_executable(test_${PROJECT_NAME} ${SOURCE_LIST})
target_link_libraries(test_${PROJECT_NAME}
    ${PROJECT_NAME}
    ${CONAN_LIBS}
)