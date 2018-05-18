cmake_minimum_required(VERSION 2.8)

project(boost)

set(boost_root ${CMAKE_CURRENT_SOURCE_DIR}/boost_1_56_0)
message([WARNING] "boost root path: " ${boost_root})

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DNO_BZIP2")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DNO_BZIP2")

include_directories(${boost_root})

file(GLOB lib_srcs ${boost_root}/libs/system/src/*.cpp)

add_library(boost_system ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/filesystem/src/*.cpp)

add_library(boost_filesystem ${lib_srcs})

set(lib_dir ${boost_root}/libs/iostreams/src)
set(lib_srcs ${lib_dir}/file_descriptor.cpp ${lib_dir}/gzip.cpp ${lib_dir}/mapped_file.cpp ${lib_dir}/zlib.cpp)

add_library(boost_iostreams ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/program_options/src/*.cpp)

add_library(boost_program_options ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/regex/src/*.cpp)

add_library(boost_regex ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/signals/src/*.cpp)

add_library(boost_signals ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/thread/src/pthread/*.cpp)

add_library(boost_thread ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/date_time/src/gregorian/*.cpp  ${boost_root}/libs/date_time/src/posix_time/*.cpp)

add_library(boost_date_time ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/atomic/src/*.cpp)

add_library(boost_atomic ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/random/src/*.cpp)

add_library(boost_random ${lib_srcs})

file(GLOB lib_srcs ${boost_root}/libs/math/src/tr1/*.cpp)
include_directories("${boost_root}/libs/math/src/tr1")

add_library(boost_math ${lib_srcs})

set(Boost_INCLUDE_DIRS ${boost_root})
set(Boost_LIBRARIES boost_filesystem boost_system boost_program_options boost_iostreams boost_date_time boost_atomic boost_random boost_math)
set(Boost_LINK_DIRS ${LIBRARY_OUTPUT_PATH})

configure_file(${CMAKE_SOURCE_DIR}/boostconfig.cmake.in
               ${CMAKE_BINARY_DIR}/boostconfig.cmake @ONLY)

install(DIRECTORY ${boost_root}/boost DESTINATION include)
install(TARGETS boost_system DESTINATION lib)
install(TARGETS boost_filesystem DESTINATION lib)
install(TARGETS boost_program_options DESTINATION lib)
install(TARGETS boost_iostreams DESTINATION lib)
install(TARGETS boost_regex DESTINATION lib)
install(TARGETS boost_signals DESTINATION lib)
install(TARGETS boost_thread DESTINATION lib)
install(TARGETS boost_date_time DESTINATION lib)
install(TARGETS boost_atomic DESTINATION lib)
install(TARGETS boost_random DESTINATION lib)
install(TARGETS boost_math DESTINATION lib)