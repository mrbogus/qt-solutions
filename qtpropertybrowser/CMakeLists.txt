CMAKE_MINIMUM_REQUIRED(VERSION 2.8.5)
cmake_policy(SET CMP0020 NEW)
include(CMakePackageConfigHelpers)

add_definitions (-DQT_DISABLE_DEPRECATED_BEFORE=0)

PROJECT(QtPropertyBrowser)

OPTION(QtPropertyBrowser_BUILD_EXAMPLES "Build examples" OFF)
OPTION(QtPropertyBrowser_BUILD_SHARED_LIBS "Build shared libraries (dll)" OFF)

#-----------------------------------------------------------------------------
# Output directories.
#
SET(output_dir ${QtPropertyBrowser_BINARY_DIR}/bin)
FOREACH(type LIBRARY RUNTIME ARCHIVE)
  IF(NOT DEFINED CMAKE_${type}_OUTPUT_DIRECTORY)
    SET(CMAKE_${type}_OUTPUT_DIRECTORY ${output_dir} CACHE INTERNAL "Single output directory for building all libraries.")
  ENDIF()
ENDFOREACH()

#-----------------------------------------------------------------------------
# Qt
#
FIND_PACKAGE(Qt5 COMPONENTS Widgets REQUIRED)

#-----------------------------------------------------------------------------
# Subdirectories
#
ADD_SUBDIRECTORY(src)
IF(QtPropertyBrowser_BUILD_EXAMPLES)
  ADD_SUBDIRECTORY(examples)
ENDIF()

SET(QtPropertyBrowser_INSTALL_DIR ${CMAKE_INSTALL_PREFIX} CACHE INTERNAL "...")

#-----------------------------------------------------------------------------
# Generate QtPropertyBrowserConfig file
#
CONFIGURE_FILE(UseQtPropertyBrowser.cmake.in
               ${QtPropertyBrowser_BINARY_DIR}/cmake/UseQtPropertyBrowser.cmake COPYONLY)

INCLUDE(GenerateQtPropertyBrowserConfig.cmake)

INSTALL (
	FILES README.TXT
	DESTINATION .
)

INSTALL (
	FILES ${QtPropertyBrowser_BINARY_DIR}/cmake/UseQtPropertyBrowser.cmake ${QtPropertyBrowser_BINARY_DIR}/cmake/QtPropertyBrowserConfig.cmake
	DESTINATION cmake
)