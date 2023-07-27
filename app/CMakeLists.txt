cmake_minimum_required(VERSION 3.16)

project(test_app)

add_executable(${PROJECT_NAME} SHARED
    src/main.cpp
)

target_link_libraries( ${PROJECT_NAME}
    test::test_lib
)

# Using c++17
set_target_properties(${PROJECT_NAME} PROPERTIES CXX_STANDARD 17)


# Set our local install directory
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/../install/" CACHE PATH "Location of the 'install' directory." FORCE)
endif()

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
