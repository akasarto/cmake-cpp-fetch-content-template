### Global Setup

# Core Project Definitions

cmake_minimum_required(VERSION 3.23)

set(PRIMARY_OUTPUT_NAME "cppFetchContentTemplate")

set(CMAKE_CXX_STANDARD              17) # https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD.html
set(CMAKE_CXX_STANDARD_REQUIRED     ON) # https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_STANDARD_REQUIRED.html
set(CMAKE_EXPORT_COMPILE_COMMANDS   ON) # https://cmake.org/cmake/help/latest/variable/CMAKE_EXPORT_COMPILE_COMMANDS.html
set(CMAKE_CXX_EXTENSIONS            OFF) # https://cmake.org/cmake/help/latest/variable/CMAKE_CXX_EXTENSIONS.html

# Setup fetch content
include(FetchContent)
# set(FETCHCONTENT_BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/deps
#     CACHE PATH "Custom dependencies folder." FORCE
# )

project("${PRIMARY_OUTPUT_NAME}" VERSION 1.0.0 LANGUAGES C CXX)

### External Dependencies

FetchContent_Declare(
    cppHelloWorld
    GIT_REPOSITORY https://github.com/akasarto/cmake-cpp-hello-world-library.git
    GIT_SHALLOW true
    GIT_TAG main
)
FetchContent_MakeAvailable(cppHelloWorld)

### Local Targets

set(PRIMARY_SOURCE_FILES
    "src/main.cpp"
)
add_executable(${PRIMARY_OUTPUT_NAME}
    ${PRIMARY_SOURCE_FILES}
)
target_link_libraries(${PRIMARY_OUTPUT_NAME} PUBLIC
    cppHelloWorld
)