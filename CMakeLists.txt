cmake_minimum_required(VERSION 3.12)
project(cadical LANGUAGES C CXX)

include(CheckSymbolExists)
check_symbol_exists(closefrom "unistd.h" CADICAL_HAVE_CLOSEFROM)

file(GLOB cadical_source_files CONFIGURE_DEPENDS
  "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
)
list(REMOVE_ITEM cadical_source_files
  "${CMAKE_CURRENT_SOURCE_DIR}/src/cadical.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/src/mobical.cpp"
)

add_library(cadical ${cadical_source_files})
target_include_directories(cadical PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
target_compile_definitions(cadical PRIVATE
  NBUILD
  QUIET
  NCONTRACTS
  NTRACING
  NCONTRIB
  NDEBUG
)

if(NOT CADICAL_HAVE_CLOSEFROM)
  target_compile_definitions(cadical PRIVATE NCLOSEFROM)
endif()
