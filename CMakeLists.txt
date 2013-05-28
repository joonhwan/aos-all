cmake_minimum_required( VERSION 2.8 )

project( ArtOfSequence )

# Make sure we use UNICODE.
add_definitions(-DUNICODE -D_UNICODE)

# Force Boost.Thread V4 use for all c++ projects, including dependencies.
add_definitions( -DBOOST_THREAD_VERSION=4 )

# Use relative paths
# This is mostly to reduce path size for command-line limits on windows
if( WIN32 )

	message( STATUS "Using relative paths (where possible) ..." )
	# This seems to break Xcode projects so definitely don't enable on Apple builds
	set( CMAKE_USE_RELATIVE_PATHS 			TRUE	CACHE BOOL "It is preferable to use relative paths on Windows compilers." )
	set( CMAKE_SUPPRESS_REGENERATION 		TRUE	CACHE BOOL "Not sure what is this feature. Option taken from OGRE." )

	if( MSVC )
		# force multi-thread compilation on Visual Studio
		set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP" )
		message( "Forced Visual Studio to allow parallel compilations (/MP). \n    Flags : " ${CMAKE_CXX_FLAGS} )
	endif()
  
endif()


set( BUILD_DIR ${CMAKE_CURRENT_BINARY_DIR}/Build )

set( EXECUTABLE_OUTPUT_PATH     ${BUILD_DIR} )
set( LIBRARY_OUTPUT_PATH        ${BUILD_DIR} )

# Of course we want unit tests possible.
enable_testing()

# Allow generating test projects if the user want it.
option( AOS_ENABLE_ALL_TESTS "Enable generation of all test projects of AOS projects" OFF )

# Add dependencies projects to make thhem visible from IDEs
add_subdirectory( dependencies )

# AOS Projects
add_subdirectory( aosl )
add_subdirectory( library )
add_subdirectory( tool )
