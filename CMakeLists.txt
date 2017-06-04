cmake_minimum_required(VERSION 3.1)

set (CMAKE_CXX_STANDARD 11)

project(wzNetClient)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
set(CONFIG_PACKAGE_LOCATION ${CMAKE_INSTALL_LIBDIR}/cmake/CapnProto)
set(CapnProto_DIR ${CMAKE_INSTALL_LIBDIR}/cmake/)
find_package(CapnProto CONFIG REQUIRED PATHS "${CMAKE_CURRENT_SOURCE_DIR}/cmake" )

capnp_generate_cpp(wzNetSources wzNetHeaders wzNet.capnp)

add_executable(${PROJECT_NAME} "main.cpp" ${wzNetSources})

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(${PROJECT_NAME} CapnProto::capnp-rpc)
