cmake_minimum_required ( VERSION 2.8 )
project ( SimpleSimulationEngine )

# ==== FLAGS

set(default_build_type Release)
if( UNIX )
    SET( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++20" )
endif()


# https://stackoverflow.com/questions/7724569/debug-vs-release-in-cmake
#message ( "CMAKE_CXX_FLAGS_DEBUG   ${CMAKE_CXX_FLAGS_DEBUG}  " )
#message ( "CMAKE_CXX_FLAGS_RELEASE ${CMAKE_CXX_FLAGS_RELEASE}" )
message ( "CMAKE_BUILD_TYPE   ${CMAKE_BUILD_TYPE}  " )
SET( IGNORE_WARRNING_FLAGS "-Wno-int-to-pointer-cast -Wno-switch -Wno-reorder -Wno-deprecated -Wno-maybe-uninitialized -Wno-char-subscripts -Wno-write-strings -Wno-format -Wno-parentheses -Wno-unused-but-set-variable  -Wno-narrowing -Wno-unused-result  -Wno-sign-compare -Wno-strict-aliasing -Wno-unused-variable -Wno-unused-value -Wno-comment -Wno-misleading-indentation " )
SET( WARRNING_TO_ERROR "-Werror=return-type -Werror=init-self -Werror=uninitialized -Werror=implicit-fallthrough -Werror=tautological-compare -Werror=delete-non-virtual-dtor")

#SET( AXULIARY_COMPILE_FLAGS "-O2 -fPIC -march=native " )
SET( AXULIARY_COMPILE_FLAGS "-g -Og -fPIC -fno-strict-aliasing ")
SET( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${AXULIARY_COMPILE_FLAGS} ${IGNORE_WARRNING_FLAGS} ${WARRNING_TO_ERROR}" )
message ( "CMAKE_CXX_FLAGS " ${CMAKE_CXX_FLAGS} )

# ==== DIRS

SET( MY_SRC_DIR    "${CMAKE_SOURCE_DIR}" )
SET( MY_BIN_SHARE  "${MY_SRC_DIR}/Build"   )

SET( SRC_CORE  "${MY_SRC_DIR}/SimSim_core" )
SET( SRC_GL1   "${MY_SRC_DIR}/SimSim_GL1"  )
SET( COMMON_RESOURCES "${SRC_GL1}/common_resources"       )

include_directories(
        ${SRC_CORE}
        ${SRC_CORE}/math
        ${SRC_CORE}/geometry
        ${SRC_CORE}/graphics
        ${SRC_CORE}/numerics
        ${SRC_CORE}/optimization
        ${SRC_CORE}/splines
        ${SRC_CORE}/physics
        ${SRC_CORE}/algorithms
        ${SRC_CORE}/datastructs
        ${SRC_CORE}/maps
        ${SRC_CORE}/utils
        ${SRC_GL1}
        ${SRC_GL1}/SDL2OGL
        ${MY_SRC_DIR}/molecular
)

set( CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake_utils )

#file (GLOB_RECURSE _ALL_SRCS_ *.h *.cpp *.c )
file (GLOB_RECURSE _COMMON_SRCS_     ${SRC_CORE}/*.h     ${SRC_CORE}/*.cpp     ${SRC_CORE}/*.c     )
file (GLOB_RECURSE _COMMON_SDL_SRCS_ ${SRC_GL1}/*.h      ${SRC_GL1}/*.cpp      ${SRC_GL1}/*.c )
file (GLOB_RECURSE _MOLECULAR_SRCS_ ${MY_SRC_DIR}/molecular/*.h      ${MY_SRC_DIR}/molecular/*.cpp      ${MY_SRC_DIR}/molecular/*.c )

# ==== BUILD TARGETS

add_subdirectory( ${SRC_CORE}                   )
add_subdirectory( ${SRC_GL1}/SDL2OGL            )
add_subdirectory( ${MY_SRC_DIR}/molecular       )
add_subdirectory( ${MY_SRC_DIR}/molecular_tests )