file(GLOB cadical_source_files "src/*.cpp")
list(REMOVE_ITEM cadical_source_files "src/cadical.cpp")
list(REMOVE_ITEM cadical_source_files "src/modical.cpp")

add_library(cadical ${cadical_source_files})
target_include_directories(cadical PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
target_compile_options(cadical PRIVATE -DNBUILD)

