cmake_minimum_required(VERSION 3.1)
project(bar VERSION 1.0 DESCRIPTION "bar library")

# Define the libraries
add_library(foo STATIC foo.cpp foo.hpp)
add_library(bar STATIC bar.cpp bar.hpp)

# Link bar to foo
target_link_libraries(bar PRIVATE foo)
