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

set(CMAKE_CXX_FLAGS "-fpermissive -Wno-array-bounds -Wno-format-truncation")

if(UNIX)
  add_definitions(-D_GNU_SOURCE)
endif()

if(WIN32)
  set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -static")
endif()

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

if (CMAKE_BUILD_TYPE MATCHES Release)
  set_target_properties(quickjs PROPERTIES LINK_FLAGS_RELEASE -s)
endif()

if(WIN32)
  set_target_properties(quickjs PROPERTIES PREFIX "")
  target_link_libraries(quickjs -static-libstdc++ -static-libgcc pthread)
else()
  target_link_libraries(quickjs -static-libstdc++ m dl pthread)
endif()

set_target_properties(quickjs
          PROPERTIES
          RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/../src/main/resources/META-INF")
