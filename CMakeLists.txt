cmake_minimum_required(VERSION 2.4.6)
set(ROS_BUILD_TYPE Release)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
rosbuild_init()
include_directories(${PROJECT_SOURCE_DIR}/code)

# Add a ROS C++ macro to tell SBPL to use ROS print statements
add_definitions(-DROS)

include_directories(src/include)

rosbuild_add_library(sbpl 
  src/discrete_space_information/environment_nav2D.cpp
  src/discrete_space_information/environment_navxythetalat.cpp
  src/discrete_space_information/environment_navxythetamlevlat.cpp
  src/discrete_space_information/environment_nav2Duu.cpp
  src/discrete_space_information/environment_XXX.cpp
  src/discrete_space_information/environment_robarm.cpp
  src/planners/araplanner.cpp
  src/planners/adplanner.cpp
  src/planners/viplanner.cpp
  src/planners/ppcpplanner.cpp
  src/planners/ANAplanner.cpp
  src/planners/rstarplanner.cpp
  src/utils/heap.cpp
  src/utils/mdp.cpp
  src/utils/utils.cpp
  src/utils/2Dgridsearch.cpp	
  )

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
rosbuild_add_executable(test_sbpl src/test/main.cpp)
target_link_libraries(test_sbpl sbpl)
rosbuild_add_executable(test_adjacency_list src/test/test_adjacency_list.cpp)
target_link_libraries(test_adjacency_list sbpl)

#set(PKG_NAME "sbpl")
#set(PKG_DESC "The Search Based Planning Library")
#set(PKG_SBPL_LIBS "-lsbpl")
#set(pkg_conf_file "${CMAKE_CURRENT_SOURCE_DIR}/sbpl.pc")
#configure_file("${pkg_conf_file}.in" "${pkg_conf_file}" @ONLY)
#install(FILES ${pkg_conf_file} DESTINATION lib/pkgconfig/ COMPONENT pkgconfig)

#install(DIRECTORY src/include/sbpl DESTINATION include
#	FILES_MATCHING PATTERN "*.h")
#install(TARGETS sbpl
#	LIBRARY DESTINATION lib)

rosbuild_add_executable(test_sbpl src/test/main.cpp)
target_link_libraries(test_sbpl sbpl)

rosbuild_add_executable(test_adjacency_list src/test/test_adjacency_list.cpp)
target_link_libraries(test_adjacency_list sbpl)
