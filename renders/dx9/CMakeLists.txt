cmake_minimum_required(VERSION 3.5)

project(RenderDX9
  LANGUAGES CXX 
  VERSION 1.0.599.0
)

set(LIBRARY_HEADERS_DIR ../src/ukncbtl-renders/${PROJECT_NAME})
set(LIBRARY_HEADERS
#  ${LIBRARY_HEADERS_DIR}/sr.h
)

set(LIBRARY_SOURCES_DIR ../src/ukncbtl-renders/${PROJECT_NAME})
set(LIBRARY_SOURCES
  ${LIBRARY_SOURCES_DIR}/stdafx.h
  ${LIBRARY_SOURCES_DIR}/stdafx.cpp
  ${LIBRARY_SOURCES_DIR}/${PROJECT_NAME}.cpp
  ${LIBRARY_SOURCES_DIR}/${PROJECT_NAME}.def
)

add_library(${PROJECT_NAME} SHARED
  ${LIBRARY_HEADERS}
  ${LIBRARY_SOURCES}
)

target_compile_definitions(${PROJECT_NAME} 
  PRIVATE UNICODE _UNICODE
)

# set_target_properties(
#   ${PROJECT_NAME} PROPERTIES WIN32_EXECUTABLE 1
# )

target_link_libraries(${PROJECT_NAME} 
  PRIVATE d3d9.lib
)

target_include_directories(${PROJECT_NAME} PRIVATE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/${PROJECT_NAME}>
  $<INSTALL_INTERFACE:include/${PROJECT_NAME}>
)

target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)
