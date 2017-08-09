cmake_minimum_required(VERSION 2.8.3)
project(hopscotch_map_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)
file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/hopscotch-map)

ExternalProject_Add(hopscotch-map_src
  URL "https://github.com/Tessil/hopscotch-map/archive/v1.4.0.tar.gz"
  INSTALL_COMMAND cd ../hopscotch-map_src/src && cp hopscotch_hash.h hopscotch_map.h hopscotch_set.h hopscotch_sc_map.h hopscotch_sc_set.h ${CATKIN_DEVEL_PREFIX}/include/hopscotch-map
)

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} hopscotch-map_src)

cs_install()

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/hopscotch-map
  CFG_EXTRAS hopscotch-map-extras.cmake)
