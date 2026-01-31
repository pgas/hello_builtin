cmake_minimum_required(VERSION 3.10)
project(hello VERSION 0.1 LANGUAGES C)

# Set C standard
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Option to specify bash headers location
set(BASH_HEADERS "/usr/include" CACHE PATH "The prefix where the bash headers are installed")

# Check for bash headers
find_path(BASH_HEADERS_FOUND builtins.h
    HINTS "${BASH_HEADERS}/bash" "${BASH_HEADERS}" "${BASH_HEADERS}/include"
    NO_DEFAULT_PATH
)

if(NOT BASH_HEADERS_FOUND)
    message(FATAL_ERROR "Unable to find the bash headers. Please use -DBASH_HEADERS=/path/to/headers/")
endif()

message(STATUS "Found bash headers at: ${BASH_HEADERS_FOUND}")

# Add subdirectory
add_subdirectory(src)
