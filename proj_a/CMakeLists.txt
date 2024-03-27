cmake_minimum_required(VERSION 3.17)

add_library(${PROJECT_NAME}_static STATIC)
add_library(${PROJECT_NAME}::static ALIAS ${PROJECT_NAME}_static)

target_sources(${PROJECT_NAME}_static PRIVATE ${PROJECT_NAME}.hpp ${PROJECT_NAME}.cpp)
