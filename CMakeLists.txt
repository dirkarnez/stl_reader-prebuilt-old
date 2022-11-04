cmake_minimum_required (VERSION 3.0.2)
project (stl_reader LANGUAGES CXX)

add_library(stl_reader INTERFACE)
target_include_directories(stl_reader INTERFACE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
    $<INSTALL_INTERFACE:include/stl_reader>
)

include(GNUInstallDirs) # define CMAKE_INSTALL_*
install(FILES stl_reader.h DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")
install(TARGETS stl_reader EXPORT stl_readerConfig)
install(EXPORT stl_readerConfig DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/stl_reader)
export(EXPORT stl_readerConfig)