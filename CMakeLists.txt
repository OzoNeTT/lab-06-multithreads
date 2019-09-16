cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(
  HUNTER_CACHE_SERVERS
  "https://github.com/bmstu-iu8-cpp-sem-3/hunter-cache"
  CACHE STRING "Default cache server"
)

include("tools/gate/cmake/HunterGate.cmake")

huntergate(
  URL "https://github.com/ruslo/hunter/archive/v0.23.34.tar.gz"
  SHA1 "70287b1ffa810ee4e952052a9adff9b4856d0d54"
)

# TODO: rename project and delete this comment
project(template)
string(APPEND CMAKE_CXX_FLAGS " -pedantic -Werror -Wall -Wextra")
string(APPEND CMAKE_CXX_FLAGS " -Wno-unused-command-line-argument")
string(APPEND CMAKE_CXX_FLAGS " -Wshadow -Wnon-virtual-dtor")

hunter_add_package(Boost COMPONENTS filesystem log system thread)
find_package(Boost CONFIG REQUIRED filesystem log log_setup system thread)
find_package(Threads)

# TODO: change template word to project name and delete this comment
add_library(template STATIC
  # enum your files and delete this comment
  ${CMAKE_CURRENT_SOURCE_DIR}/sources/source.cpp
)

# TODO: change template word to project name and delete this comment
target_include_directories(template 
  PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# TODO: change template word to project name and delete this comment
target_link_libraries(
        ${PROJECT_NAME}
        ${CMAKE_THREAD_LIBS_INIT}
        Boost::log_setup
        Boost::log
        Boost::thread
        Boost::filesystem
        Boost::system
)