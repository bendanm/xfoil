#############################################################################
#
#  XFOIL
#
#  Copyright (C) 2000 Mark Drela
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 2 of the License, or
#  (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
#############################################################################

cmake_minimum_required(VERSION 3.5)
project(xfoil LANGUAGES C Fortran VERSION 6.97)

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE Release CACHE STRING
    "Choose the type of build; options are Debug Release RelWithDebInfo MinSizeRel"
    FORCE)
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY
    STRINGS
      Debug
      Release
      RelWithDebInfo
      MinSizeRel)
endif()

include(CTest)

if(CMAKE_Fortran_COMPILER_ID STREQUAL GNU)
  set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -std=legacy")
endif()

option(DOUBLE_PRECISION
  "Make the real and complex types eight bytes long" OFF)

if(DOUBLE_PRECISION)
  if(CMAKE_Fortran_COMPILER_ID STREQUAL Intel)
    if(WIN32)
      set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} /real-size:64")
    else()
      set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -real-size 64")
    endif()
  elseif(CMAKE_Fortran_COMPILER_ID STREQUAL GNU)
    set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -fdefault-real-8")
  endif()
endif()

include(GNUInstallDirs)

set(ORRS_DIR "${CMAKE_SOURCE_DIR}/orrs")

add_subdirectory(orrs)
add_subdirectory(osrc)
add_subdirectory(plotlib)
add_subdirectory(src)

set(XFOIL_DOCS version_notes.txt xfoil_doc.txt)
install(FILES ${XFOIL_DOCS} DESTINATION ${CMAKE_INSTALL_DOCDIR})

include(CMakePackageConfigHelpers)

configure_package_config_file(xfoil-config.cmake.in xfoil-config.cmake.in
  INSTALL_DESTINATION ${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME}
  PATH_VARS CMAKE_INSTALL_BINDIR
  NO_SET_AND_CHECK_MACRO NO_CHECK_REQUIRED_COMPONENTS_MACRO)

file(GENERATE
  OUTPUT xfoil-config.cmake
  INPUT "${CMAKE_CURRENT_BINARY_DIR}/xfoil-config.cmake.in")

write_basic_package_version_file(xfoil-config-version.cmake
  COMPATIBILITY SameMajorVersion)

install(FILES
  "${CMAKE_CURRENT_BINARY_DIR}/xfoil-config.cmake"
  "${CMAKE_CURRENT_BINARY_DIR}/xfoil-config-version.cmake"
  DESTINATION ${CMAKE_INSTALL_DATADIR}/${PROJECT_NAME})

include(CPack)
