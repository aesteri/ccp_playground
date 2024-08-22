cmake_minimum_required(VERSION 3.1)
project(
    ccp_playground VERSION 1.0
                  DESCRIPTION "Playing around with cmake"
)


# Specify the path to the installed bar library
if (NOT DEFINED CMAKE_PREFIX_PATH)
    set(PATH "/usr/local/lib/cmake/bar" CACHE PATH "Path to prebuilt bar library" FORCE)
endif()

set(CMAKE_PREFIX_PATH "/usr/local" CACHE PATH "Path to prebuilt bar library" FORCE)

find_package(bar REQUIRED)

#declare executable
add_executable(target playing.cpp)

#link together
target_link_libraries(target PUBLIC bar::bar)


target_include_directories(target PUBLIC
                          "${PROJECT_BINARY_DIR}"
                          "${PROJECT_SOURCE_DIR}/bar"
                          )

# be sure that you use the generator expressions
# ($<BUILD_INTERFACE: and $<INSTALL_INTERFACE:) for your include directory setups
target_include_directories(target PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
set_target_properties(target PROPERTIES CXX_STANDARD 17)
target_compile_features(target PUBLIC cxx_std_17)

# Install the executable to bin directory
install(TARGETS target DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)

