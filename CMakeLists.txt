cmake_minimum_required(VERSION 3.5)

project(ukncbtl-cmake)

#set(CMAKE_CXX_STANDARD 17)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)

set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

cmake_policy(SET CMP0069 NEW) 
set(CMAKE_POLICY_DEFAULT_CMP0069 NEW)

# seems to be that ukncbtl wouldn't build without UNICODE
set_directory_properties(PROPERTIES 
  COMPILE_DEFINITIONS "UNICODE;_UNICODE" 
  INTERPROCEDURAL_OPTIMIZATION_RELWITHDEBINFO "TRUE"
  LINK_OPTIONS "/PROFILE"
)

add_subdirectory(ukncbtl)
add_subdirectory(renders)
