# Copyright (C) 2009 Leandro Lisboa Penz <lpenz@lpenz.org>
# This file is subject to the terms and conditions defined in
# file 'LICENSE', which is part of this source code package.

cmake_minimum_required (VERSION 3.0)

project (gkrellm-sdnotify)

if(CMAKE_COMPILER_IS_GNUCXX)
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror -W")
endif(CMAKE_COMPILER_IS_GNUCXX)

find_package (PkgConfig REQUIRED)
pkg_check_modules (GLIB REQUIRED glib-2.0)
pkg_check_modules (GTK2 REQUIRED gtk+-2.0)
pkg_check_modules (SYSTEMD REQUIRED libsystemd)

include_directories ("${GLIB_INCLUDE_DIRS}")
include_directories ("${GTK2_INCLUDE_DIRS}")

add_library (gkrellm-sdnotify
  SHARED
  gkrellm-sdnotify.cc)

target_link_libraries (gkrellm-sdnotify ${SYSTEMD_LIBRARIES})

install (TARGETS gkrellm-sdnotify
  DESTINATION lib/gkrellm2/plugins
  )
