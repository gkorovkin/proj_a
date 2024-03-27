cmake_minimum_required(VERSION 3.17)

include(CMakePackageConfigHelpers)

add_library(${PROJECT_NAME}_static STATIC)
add_library(${PROJECT_NAME}::static ALIAS ${PROJECT_NAME}_static)

target_sources(${PROJECT_NAME}_static PRIVATE ${PROJECT_NAME}.hpp ${PROJECT_NAME}.cpp)

set(targets_export_name proj_a_static)

configure_package_config_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/proj_a.cmake.in
	${PROJECT_BINARY_DIR}/proj_a.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/proj_a)

export(TARGETS ${PROJECT_NAME}_static NAMESPACE proj_a::
    FILE ${PROJECT_BINARY_DIR}/${targets_export_name}.cmake)

install(FILES proj_a.hpp DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/proj_a)

# Install the library and headers.
install(TARGETS ${PROJECT_NAME}_static EXPORT proj_a-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
