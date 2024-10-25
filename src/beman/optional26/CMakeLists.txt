# cmake-format: off
# src/beman/optional26/CMakeLists.txt -*-makefile-*-
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception
# cmake-format: on

file(GLOB optional26_headers CONFIGURE_DEPENDS "beman/optional26/*.hpp")
add_library(beman_optional26 STATIC)
target_sources(beman_optional26
  PRIVATE
    optional.cpp
    detail/iterator.cpp
  PUBLIC
    FILE_SET headers
    TYPE HEADERS
    BASE_DIRS .
    FILES ${optional26_headers}
)

target_include_directories(
  beman_optional26
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../../../include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../../../src/>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/${CMAKE_LOWER_PROJECT_NAME}>
)

install(
  TARGETS beman_optional26
  EXPORT ${TARGETS_EXPORT_NAME}
  DESTINATION ${CMAKE_INSTALL_LIBDIR}
  FILE_SET headers
)

string(TOLOWER ${CMAKE_PROJECT_NAME} CMAKE_LOWER_PROJECT_NAME)

target_link_libraries(beman_optional26)

# Tests
if(BUILD_TESTING)
  add_subdirectory(tests)
endif()
