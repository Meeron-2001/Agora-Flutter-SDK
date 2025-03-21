cmake_minimum_required(VERSION 3.4.1)

# Define the library
add_library(
    iris_rendering_android
    SHARED
    src/main/cpp/iris_rtc_rendering_android.cc
)

# Specify include directories
include_directories(
    src/main/cpp
)

# Find and link required Android libraries
find_library(log-lib log)
find_library(android-lib android)
find_library(gles-lib GLESv2)
find_library(egl-lib EGL)

# Enable C++ exceptions and RTTI
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -frtti")

# Use the shared C++ runtime library
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -lc++_shared")

# Link the libraries
target_link_libraries(
    iris_rendering_android
    ${log-lib}
    ${android-lib}
    ${gles-lib}
    ${egl-lib}
    -latomic
    -lm
)