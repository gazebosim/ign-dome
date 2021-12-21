cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)

#============================================================================
# Initialize the project
#============================================================================
project(ignition-dome VERSION 1.0.1)

#============================================================================
# Find ignition-cmake
#============================================================================
# If you get an error at this line, you need to install ignition-cmake
find_package(ignition-cmake2 2.9.0 REQUIRED)

#============================================================================
# Configure the project
#============================================================================
ign_configure_project(VERSION_SUFFIX)

# all list of dome packages

ign_find_package(ignition-common3 REQUIRED VERSION 3.14.0)
ign_find_package(ignition-fuel_tools5 REQUIRED VERSION 5.2.0)
ign_find_package(ignition-gazebo4 REQUIRED VERSION 4.14.0)
ign_find_package(ignition-gui4 REQUIRED VERSION 4.6.0)
ign_find_package(ignition-launch3 REQUIRED VERSION 3.4.2)
ign_find_package(ignition-math6 REQUIRED VERSION 6.9.2)
ign_find_package(ignition-msgs6 REQUIRED VERSION 6.6.1)
ign_find_package(ignition-physics3 REQUIRED VERSION 3.4.1)
ign_find_package(ignition-plugin1 REQUIRED VERSION 1.2.1)
ign_find_package(ignition-rendering4 REQUIRED VERSION 4.9.1)
ign_find_package(ignition-sensors4 REQUIRED VERSION 4.3.0)
ign_find_package(ignition-tools REQUIRED VERSION 1.4.1)
ign_find_package(ignition-transport9 REQUIRED VERSION 9.2.0)
ign_find_package(sdformat10 REQUIRED VERSION 10.6.1)

if(build_warnings)
  set(all_warnings " CONFIGURATION WARNINGS:")
  foreach (msg ${build_warnings})
    ign_string_append(all_warnings " -- ${msg}" DELIM "\n")
  endforeach ()
  message(WARNING "${all_warnings}")
endif (build_warnings)

if(build_errors)
  message(SEND_ERROR "-- BUILD ERRORS: These must be resolved before compiling.")
  foreach(msg ${build_errors})
    message(SEND_ERROR "-- ${msg}")
  endforeach()
  message(SEND_ERROR "-- END BUILD ERRORS\n")

  set(error_str "Errors encountered in build. Please see BUILD ERRORS above.")

  message(FATAL_ERROR "${error_str}")

endif()

install(DIRECTORY gazebodistro DESTINATION ${IGN_DATA_INSTALL_DIR})
