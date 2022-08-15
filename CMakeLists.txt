cmake_minimum_required(VERSION 3.9)
project(EXTENSION_NAME VERSION 0.0.1 LANGUAGES CXX)

# [TO ADAPT] To make DLL export work, you have to put the .dll file next
# to the executable or other dynamic linked library files of the engine.
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin) 

set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

# C++ standard can be overridden when this is used as a sub-project.
if(NOT CMAKE_CXX_STANDARD)
  # This project is using C++20
  set(CMAKE_CXX_STANDARD 20)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  set(CMAKE_CXX_EXTENSIONS OFF)
endif(NOT CMAKE_CXX_STANDARD)

include_directories(${PROJECT_SOURCE_DIR/})

IF (CMAKE_SYSTEM_NAME MATCHES "windows")
  add_definitions(-DBASE_EXPORTS)
ENDIF()

add_library(${PROJECT_NAME} SHARED
  # Put all of your source files there.
  "public/EXTENSION_NAME/my_public_api.cc"
  "public/EXTENSION_NAME/my_public_api.h"

  "private/EXTENSION_NAME/my_private_api.cc"
  "private/EXTENSION_NAME/my_private_api.h"
)

set_target_properties(EXTENSION_NAME PROPERTIES LINKER_LANGUAGE CXX)

target_include_directories(${PROJECT_NAME}
  PUBLIC
    $<INSTALL_INTERFACE:/public>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/public>
  PRIVATE
    $<INSTALL_INTERFACE:/private>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/private>
)