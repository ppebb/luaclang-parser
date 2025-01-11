cmake_minimum_required(VERSION 2.6)
project(luaclang CXX)

find_package(Lua51 REQUIRED)
find_library(CLANG_LIBRARY NAMES clang libclang)
find_library(CLANG_CPP_LIBRARY NAMES clang-cpp libclang-cpp)

if(APPLE)
   set(CMAKE_SHARED_MODULE_CREATE_CXX_FLAGS
       "${CMAKE_SHARED_MODULE_CREATE_CXX_FLAGS} -flat_namespace -undefined dynamic_lookup")
endif(APPLE)

include_directories(${LUA_INCLUDE_DIR})
add_library(luaclang-parser MODULE luaclang-parser.cpp)
target_link_libraries(luaclang-parser ${CLANG_LIBRARY} ${CLANG_CPP_LIBRARY})
set_target_properties(luaclang-parser PROPERTIES PREFIX "")
