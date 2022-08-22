cmake_minimum_required(VERSION 3.5)

project(ukncbtl-cmake)

#set(CMAKE_CXX_STANDARD 17)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)

set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

# seems to be that ukncbtl wouldn't build without UNICODE
set_directory_properties(PROPERTIES COMPILE_DEFINITIONS "UNICODE;_UNICODE")

#set_directory_properties(PROPERTIES LINK_FLAGS "/PROFILE")

add_subdirectory(ukncbtl)
add_subdirectory(renders)
