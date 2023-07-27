cmake_minimum_required(VERSION 3.16)

# The project namespace
set(PROJECT_NAMESPACE test)

# The name of the component
set(COMPONENT_NAME test_lib)

project(${PROJECT_NAMESPACE}_${COMPONENT_NAME})

add_library(${COMPONENT_NAME} SHARED
    src/interface.cpp
)

target_include_directories( ${COMPONENT_NAME}
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/>
        $<INSTALL_INTERFACE:include/>
)

# Using c++17
set_target_properties(${COMPONENT_NAME} PROPERTIES CXX_STANDARD 17)

# Add an alias to tell future "target_link_libraries()" calls this is a target, and never a linker flag
add_library(${PROJECT_NAMESPACE}::${COMPONENT_NAME} ALIAS ${COMPONENT_NAME})

# Set our local install directory
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/../install/" CACHE PATH "Location of the 'install' directory." FORCE)
endif()

# Install the targets associated with the ${PROJECT_NAME} (binaries, static libraries and/or shared libraries)
install(TARGETS ${COMPONENT_NAME} EXPORT ${COMPONENT_NAME}_targets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

# Install Header files
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
