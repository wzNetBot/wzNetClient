cmake_minimum_required(VERSION 3.1)

set (CMAKE_CXX_STANDARD 11)

project(wzNetClient)

find_package(CapnProto CONFIG REQUIRED )

capnp_generate_cpp(wzNetSources wzNetHeaders wzNet.capnp)

add_executable(${PROJECT_NAME} "main.cpp" ${wzNetSources})

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(${PROJECT_NAME} CapnProto::capnp-rpc)
