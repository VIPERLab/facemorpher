cmake_minimum_required(VERSION 3.3)
project(face-morpher)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
find_package( OpenCV REQUIRED core imgproc objdetect photo )
include_directories( ${OpenCV_INCLUDE_DIRS} )

#Internal files
GENERATE_PROJECT_STRUCTURE_VARIABLE()
install_files(${CMAKE_RUNTIME_OUTPUT_DIRECTORY} FILES "src/triangles.txt")
add_library(${PROJECT_NAME} SHARED ${${PROJECT_NAME}_FILES})
target_link_libraries( ${PROJECT_NAME} ${OpenCV_LIBS} face-landmark-detector)
target_include_directories(${PROJECT_NAME} PUBLIC ${${PROJECT_NAME}_INCLUDES_DIR})
target_include_directories(${PROJECT_NAME} PRIVATE ${${PROJECT_NAME}_HEADERS_DIR})
add_dependencies (${PROJECT_NAME} face-landmark-detector)