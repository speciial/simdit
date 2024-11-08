cmake_minimum_required(VERSION 3.16)

set( CMAKE_C_STANDARD 11 )
set( CMAKE_C_STANDARD_REQUIRED ON )

# Put executable into bin directory
set( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin )
set( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/bin )
set( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/bin )

project( simdit VERSION 1.0 )

# Compiler specific settings
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -Wpedantic)

    # Linking libm for compiling on unix 
    find_library(MATH_LIBRARY m)
    if(MATH_LIBRARY)
        target_link_libraries( ${PROJECT_NAME} PUBLIC ${MATH_LIBRARY})
    endif()
endif()

add_subdirectory( source )
add_subdirectory( test )