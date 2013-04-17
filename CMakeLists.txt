cmake_minimum_required( VERSION 2.8 )

project( ArtOfSequence )

# Make sure we use UNICODE.
add_definitions(-DUNICODE -D_UNICODE)

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


add_subdirectory( aosl )
add_subdirectory( library )
add_subdirectory( tool )
