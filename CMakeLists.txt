cmake_minimum_required(VERSION 3.2)

include(cmake/HunterGate.cmake)
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.23.177.tar.gz"
    SHA1 "c3d4bf987a1c5f8ce9bb8b2b80bc6c123185cd66"
    LOCAL
)

project(opencv_ffmpeg_test)

hunter_add_package(OpenCV)
find_package(OpenCV REQUIRED)

add_executable(foo foo.cpp)
target_link_libraries(foo PRIVATE ${OpenCV_LIBS})

set(output "${CMAKE_CURRENT_BINARY_DIR}/__output")
file(MAKE_DIRECTORY "${output}")

enable_testing()
add_test(
    NAME
    foo
    COMMAND
    foo
    ${CMAKE_CURRENT_LIST_DIR}/sample_iPod.m4v
    ${output}
)
