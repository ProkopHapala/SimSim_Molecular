find_package( OpenGL REQUIRED )
find_package( GLU    REQUIRED )
find_package( SDL2   REQUIRED )

project(molecular_all)

add_subdirectory (molecular_tests)
add_subdirectory (molecular)
