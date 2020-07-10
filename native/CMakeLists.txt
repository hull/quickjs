cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_CXX_STANDARD 11)
set(BUILD_SHARED_LIBS ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

project(quickjs)

find_package(JNI REQUIRED)

message(STATUS "JNI_INCLUDE_DIRS=${JNI_INCLUDE_DIRS}")
message(STATUS "JNI_LIBRARIES=${JNI_LIBRARIES}")
message(STATUS "JAVA_INCLUDE_PATH=${JAVA_INCLUDE_PATH}")
message(STATUS "JAVA_INCLUDE_PATH2=${JAVA_INCLUDE_PATH2}")

include_directories(${JAVA_INCLUDE_PATH})
include_directories(${JAVA_INCLUDE_PATH2})

set(CMAKE_CXX_FLAGS "-fpermissive")

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -static")

file(GLOB quickjs_SRC
  "quickjs/*.h"
  "quickjs/*.cpp"
  "quickjs/quickjs.c"
  "quickjs/libbf.c"
  "quickjs/quickjs-libc.c"
  "quickjs/libunicode.c"
  "quickjs/libregexp.c"
  "quickjs/cutils.c"
)

add_definitions(-DCONFIG_VERSION="2020-07-05")

add_library(quickjs SHARED
                  ${quickjs_SRC})

target_link_libraries(quickjs -static-libstdc++ -static-libgcc pthread)