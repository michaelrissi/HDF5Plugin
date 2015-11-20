cmake_minimum_required(VERSION 2.8)
project(hdf5lz4)

find_package(HDF5 REQUIRED NO_MODULE)

include_directories(${HDF5_INCLUDE_DIR})

set(SOURCES
    h5zlz4.c
    lz4.c)

if (NOT MSVC)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")
endif()

add_library(h5lz4 SHARED ${SOURCES})

if (MSVC)
    target_link_libraries(hdf5lz4 ws2_32)
endif()
install(TARGETS hdf5lz4 RUNTIME DESTINATION bin)
