cmake_minimum_required(VERSION 2.8.4)

project(SDL_nmix)
set(NMIX_VERSION 1.1.0)
set(LIBRARY_OUTPUT_NAME "SDL2_nmix")
set(OUTPUT_DIR "SDL2_nmix")

set(NMIX_HDRS
    sdl_nmix.h
    sdl_nmix_file.h
)

set(NMIX_SRCS
    sdl_nmix.c
    sdl_nmix_file.c
)

if(WIN32)
    set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/scripts")
endif(WIN32)

find_package(SDL2 REQUIRED)

option(NMIX_BUILD_STATIC "Build static library" FALSE)
option(NMIX_BUILD_SHARED "Build shared library" TRUE)

add_definitions("-Wall -pedantic")

if(NOT WIN32)
    add_definitions("-fPIC")
endif(NOT WIN32)

if(NMIX_BUILD_SHARED)
    add_library(
        SDLnmix_shared SHARED
        ${NMIX_HDRS}
        ${NMIX_SRCS}
    )

    target_link_libraries(
        SDLnmix_shared
    )
    
    set_target_properties(SDLnmix_shared PROPERTIES OUTPUT_NAME ${LIBRARY_OUTPUT_NAME})
    set_target_properties(SDLnmix_shared PROPERTIES CLEAN_DIRECT_OUTPUT 1)
    set_target_properties(SDLnmix_shared PROPERTIES VERSION ${NMIX_VERSION})
    set_target_properties(SDLnmix_shared PROPERTIES LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${OUTPUT_DIR}/")
    set_target_properties(SDLnmix_shared PROPERTIES ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${OUTPUT_DIR}/")
    set_target_properties(SDLnmix_shared PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${OUTPUT_DIR}/")    
    set_target_properties(SDLnmix_shared PROPERTIES LINKER_LANGUAGE C)
endif(NMIX_BUILD_SHARED)

if(NMIX_BUILD_STATIC)
    add_library(
        SDLnmix_static STATIC
        ${NMIX_HDRS}
        ${NMIX_SRCS}
    )

    target_link_libraries(
        SDLnmix_static
    )
    
    set_target_properties(SDLnmix_static PROPERTIES OUTPUT_NAME ${LIBRARY_OUTPUT_NAME})
    set_target_properties(SDLnmix_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)
    set_target_properties(SDLnmix_static PROPERTIES VERSION ${NMIX_VERSION})
    set_target_properties(SDLnmix_static PROPERTIES LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${OUTPUT_DIR}/")
    set_target_properties(SDLnmix_static PROPERTIES ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${OUTPUT_DIR}/")
    set_target_properties(SDLnmix_static PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/${OUTPUT_DIR}/")    
    set_target_properties(SDLnmix_static PROPERTIES LINKER_LANGUAGE C)
    
    set_target_properties(SDLnmix_static PROPERTIES LINKER_LANGUAGE C)
endif(NMIX_BUILD_STATIC)

