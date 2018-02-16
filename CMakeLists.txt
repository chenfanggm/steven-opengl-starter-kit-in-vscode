# project
cmake_minimum_required(VERSION 3.0)
project(opengl-starter VERSION 0.0.1)

# set path of find modules
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules")

# sources
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/libs")
set(SOURCE "${SRC_DIR}/main.cpp" "${SRC_DIR}/shader.h")

# executable
add_executable(${PROJECT_NAME} ${SOURCE})
target_include_directories(${PROJECT_NAME} PRIVATE "${SRC_DIR}")
target_include_directories(${PROJECT_NAME} PRIVATE "${LIB_DIR}")
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)

# OPENGL
find_package(OpenGL REQUIRED)
if (OPENGL_FOUND)
    message("Found OPENGL at ${OPENGL_INCLUDE_DIR}")
    message("Link OPENGL libs at ${OPENGL_gl_LIBRARY}")
    target_include_directories(${PROJECT_NAME} PRIVATE ${OPENGL_INCLUDE_DIR})
    target_link_libraries(${PROJECT_NAME} PRIVATE ${OPENGL_gl_LIBRARY})
endif()

# GLEW
find_package(GLEW REQUIRED)
if (GLEW_FOUND)
    message("Found GLEW at ${GLEW_INCLUDE_DIRS}")
    message("Link GLEW libs at ${GLEW_LIBRARIES}")
    target_include_directories(${PROJECT_NAME} PRIVATE ${GLEW_INCLUDE_DIRS})
    target_link_libraries(${PROJECT_NAME} PRIVATE ${GLEW_LIBRARIES})
endif()

# GLFW
find_package(glfw3 REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE glfw)

# GLM
find_package(GLM)
if (GLM_FOUND)
  target_include_directories(${PROJECT_NAME} PRIVATE ${GLM_INCLUDE_DIR})
endif()

message("Processing CMakeLists.txt")
