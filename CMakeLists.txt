cmake_minimum_required(VERSION 3.16)

project(test_project)

if(MSVC)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
    set(BUILD_SHARED_LIBS TRUE)
endif()

add_subdirectory(./libraries/test-lib)
add_subdirectory(./app)
