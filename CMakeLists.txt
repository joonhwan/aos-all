cmake_minimum_required( VERSION 2.8 )

project( ArtOfSequence )


set( BUILD_DIR ${CMAKE_CURRENT_BINARY_DIR}/Build )

set( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${BUILD_DIR} )
set( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${BUILD_DIR} )
set( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${BUILD_DIR} )


set( AOS_TEST_PROJECTS_GROUP_PATH tests )

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
