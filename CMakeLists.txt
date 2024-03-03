cmake_minimum_required(VERSION 3.10)
project(GLEWImmediateInterface)

# Specify C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# OpenGL policy
cmake_policy(SET CMP0072 NEW)
set(OpenGL_GL_PREFERENCE GLVND)

# Find packages
find_package(glfw3 3.3 REQUIRED)
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED) # Find GLEW package

# Include directories
include_directories(${glfw_INCLUDE_DIRS})
include_directories(${GLEW_INCLUDE_DIRS}) # Include GLEW directories
include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/external)
include_directories(${CMAKE_SOURCE_DIR}/../imgui-1.90.4)
include_directories(${CMAKE_SOURCE_DIR}/../imgui-1.90.4/backends)
include_directories(${CMAKE_SOURCE_DIR}/../glm)

# Add source files
file(GLOB CPP_FILES ${CMAKE_SOURCE_DIR}/source/*.cpp)
# file(GLOB GLAD_SOURCES ${CMAKE_SOURCE_DIR}/external/glad/*.c) # Not needed for GLEW
file(GLOB IMGUI_SOURCES ${CMAKE_SOURCE_DIR}/../imgui-1.90.4/*.cpp)

# Specifically add only the necessary ImGui backend files
set(IMGUI_BACKENDS_SOURCES 
    ${CMAKE_SOURCE_DIR}/../imgui-1.90.4/backends/imgui_impl_glfw.cpp
    ${CMAKE_SOURCE_DIR}/../imgui-1.90.4/backends/imgui_impl_opengl3.cpp)

# Define the executable
add_executable(executable ${CPP_FILES} ${IMGUI_SOURCES} ${IMGUI_BACKENDS_SOURCES})

# Link libraries
target_link_libraries(executable glfw ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES}) # Link GLEW libraries
