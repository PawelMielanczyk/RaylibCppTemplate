# CMakeList.txt : CMake project for RaylibCppSetup, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("RaylibCppSetup")

# raylib
find_package(raylib QUIET)
if (NOT raylib_FOUND)
    include(FetchContent)
    FetchContent_Declare(
        raylib
        GIT_REPOSITORY https://github.com/raysan5/raylib.git
        GIT_TAG 4.5.0
    )
    FetchContent_MakeAvailable(raylib)
endif()

# raylib-cpp
find_package(raylib_cpp QUIET)
if (NOT raylib_cpp_FOUND)
    include(FetchContent)
    FetchContent_Declare(
        raylib_cpp
        GIT_REPOSITORY https://github.com/RobLoach/raylib-cpp.git
        GIT_TAG v4.5.1
    )
    FetchContent_MakeAvailable(raylib_cpp)
endif()

# Add source to this project's executable.
set(SOURCES Main.cpp)
add_executable(${PROJECT_NAME} ${SOURCES})
set_target_properties(${PROJECT_NAME} PROPERTIES CXX_STANDARD 11)
target_link_libraries(${PROJECT_NAME} PUBLIC raylib raylib_cpp)


if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET RaylibCppSetup PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.
