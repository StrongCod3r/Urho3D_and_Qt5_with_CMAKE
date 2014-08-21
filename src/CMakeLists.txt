project(QtAndUrho3D)
# Define target name
set(TARGET_NAME ${PROJECT_NAME})


#-----------------------------
# URHO3D SDK
#-----------------------------
# CMake modules: define enviroment variable "URHO3D_HOME" or define inline
#set($ENV{URHO3D_HOME} "C://Urho3D-master")
set(CMAKE_MODULE_PATH $ENV{URHO3D_HOME}/Source/CMake/Modules CACHE PATH "Path to Urho3D-specific CMake modules")

# Include Urho3D Cmake common module
include(Urho3D-CMake-common)
# Find Urho3D library
find_package(Urho3D REQUIRED)
include_directories(${URHO3D_INCLUDE_DIRS})



#-----------------------------
# Qt5 SDK
#-----------------------------
# CMake modules: define enviroment variable "CMAKE_PREFIX_PATH" or define inline
#set(CMAKE_PREFIX_PATH "C://Qt//Qt5.3.1_64//5.3//msvc2013_64_opengl" CACHE PATH "Path to Qt5-specific CMake modules")

set(CMAKE_INCLUDE_CURRENT_DIR ON)
#set(CMAKE_AUTOMOC ON)
add_definitions(${QT_DEFINITIONS})

find_package(Qt5Core REQUIRED)
find_package(Qt5Widgets REQUIRED)



#-----------------------------]
# Define source files
define_source_files ()
#------------------------------------------------------------------------------

file(GLOB UI_FILES "ui/*.ui")
file(GLOB QRC_FILES "res/*.qrc")


qt5_wrap_ui(UI_HEADERS ${UI_FILES})
qt5_add_resources(RCC_FILES ${QRC_FILES})
qt5_wrap_cpp( MOC_FILES ${H_FILES} )


# Resource for Windows
if(WIN32)
    set(SOURCE_FILES ${SOURCE_FILES} "res/app.rc")
endif()


set(SOURCE_FILES ${SOURCE_FILES} ${MOC_FILES} ${UI_HEADERS} ${RCC_FILES})

#------------------------------------------------------------------------------
# Setup target with resource copying
setup_main_executable()
#-----------------------------]


# Qt5 add modules
qt5_use_modules(${PROJECT_NAME} Core Widgets)
#target_link_libraries(${TARGET_NAME} ${QT_LIBRARIES})
