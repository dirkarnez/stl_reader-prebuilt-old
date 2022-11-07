cmake_minimum_required (VERSION 3.0.2)




file(READ "stl_reader.h" GLM_SETUP_FILE)
string(REGEX MATCH "#define[ ]+GLM_VERSION_MAJOR[ ]+([0-9]+)" _ ${GLM_SETUP_FILE})
set(GLM_VERSION_MAJOR "${CMAKE_MATCH_1}")
string(REGEX MATCH "#define[ ]+GLM_VERSION_MINOR[ ]+([0-9]+)" _ ${GLM_SETUP_FILE})
set(GLM_VERSION_MINOR "${CMAKE_MATCH_1}")
string(REGEX MATCH "#define[ ]+GLM_VERSION_PATCH[ ]+([0-9]+)" _ ${GLM_SETUP_FILE})
set(GLM_VERSION_PATCH "${CMAKE_MATCH_1}")
string(REGEX MATCH "#define[ ]+GLM_VERSION_REVISION[ ]+([0-9]+)" _ ${GLM_SETUP_FILE})
set(GLM_VERSION_REVISION "${CMAKE_MATCH_1}")

set(GLM_VERSION ${GLM_VERSION_MAJOR}.${GLM_VERSION_MINOR}.${GLM_VERSION_PATCH}.${GLM_VERSION_REVISION})
project(stl_reader VERSION ${GLM_VERSION} LANGUAGES CXX)
message(STATUS "GLM: Version " ${GLM_VERSION})


add_library(stl_reader INTERFACE)
target_include_directories(stl_reader INTERFACE
	$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
	$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

include(GNUInstallDirs) # define CMAKE_INSTALL_*
install(FILES stl_reader.h DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")
install(TARGETS stl_reader EXPORT stl_readerConfig)
install(EXPORT stl_readerConfig DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/stl_reader)
include(CMakePackageConfigHelpers)
write_basic_package_version_file("stl_readerConfigVersion.cmake" COMPATIBILITY AnyNewerVersion)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/stl_readerConfigVersion.cmake DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/stl_reader)

# export(EXPORT stl_readerConfig)
