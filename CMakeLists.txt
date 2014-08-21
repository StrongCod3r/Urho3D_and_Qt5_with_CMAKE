cmake_minimum_required(VERSION 3.0)
if(COMMAND cmake_policy)
    cmake_policy(SET CMP0003 NEW)
    if(CMAKE_VERSION VERSION_GREATER 2.8.12 OR CMAKE_VERSION VERSION_EQUAL 2.8.12)
	cmake_policy(SET CMP0022 NEW) # INTERFACE_LINK_LIBRARIES defines the link interface
    endif ()
    if(CMAKE_VERSION VERSION_GREATER 3.0.0 OR CMAKE_VERSION VERSION_EQUAL 3.0.0)
	cmake_policy(SET CMP0026 OLD) # Disallow use of the LOCATION target property - therefore we set to OLD as we still need it
	cmake_policy(SET CMP0042 NEW) # MACOSX_RPATH is enabled by default
    endif()
endif()


add_subdirectory(src)
