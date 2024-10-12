PROJECT(sqlite3
        LANGUAGES C CXX
        VERSION 3.37)
cmake_minimum_required(VERSION 3.22)

add_definitions(-DSQLITE_ENABLE_RTREE)
add_definitions(-DSQLITE_ENABLE_FTS4)
add_definitions(-DSQLITE_ENABLE_FTS5)
add_definitions(-DSQLITE_ENABLE_JSON1)
add_definitions(-DSQLITE_ENABLE_RBU)
add_definitions(-DSQLITE_ENABLE_STAT4)

add_library(SQLite3 STATIC)
add_library(SQLite::SQLite3 ALIAS SQLite3)
set_property(TARGET SQLite3 PROPERTY POSITION_INDEPENDENT_CODE ON)
target_sources(SQLite3
        PUBLIC
        FILE_SET HEADERS BASE_DIRS src FILES
        src/sqlite3.h
        src/sqlite3ext.h
        PRIVATE
        src/sqlite3.c)

add_executable(sqlite)
target_sources(sqlite
        PRIVATE
        src/shell.c)
target_link_libraries(sqlite SQLite3)
