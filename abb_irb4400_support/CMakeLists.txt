cmake_minimum_required(VERSION 2.8.3)

project(abb_irb4400_support)

find_package(catkin REQUIRED)

catkin_package()

if (CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)
  roslaunch_add_file_check(tests/roslaunch_test.xml
  	DEPENDENCIES
  	# not nice, but industrial_robot_client doesn't prefix its targets
  	joint_trajectory_action
  	abb_driver_robot_state
  	abb_driver_motion_download_interface)
endif()

foreach(dir config launch meshes urdf)
   install(DIRECTORY ${dir}/
      DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach()
