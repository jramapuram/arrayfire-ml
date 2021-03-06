CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(ARRAYFIRE_ML)

SET_PROPERTY(GLOBAL PROPERTY USE_FOLDERS ON)
ADD_DEFINITIONS(-Wall -std=c++11 -fvisibility=hidden)

OPTION(BUILD_TEST "Build Tests" ON)

# Header files
IF(NOT DEFINED AFML_INSTALL_INC_DIR)
  SET(AFML_INSTALL_INC_DIR "include" CACHE PATH "Installation path for headers")
ENDIF()

IF (BUILD_TEST)
  FILE(GLOB FILES "test/*.cpp")
  INCLUDE("${CMAKE_CURRENT_SOURCE_DIR}/AFBuildMacros.cmake")
  BUILD_ALL("${FILES}")
ENDIF()

INSTALL(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/include/" DESTINATION "${AFML_INSTALL_INC_DIR}"
  COMPONENT headers
  FILES_MATCHING
  PATTERN "*.h"
  PATTERN "*.hpp"
  PATTERN ".gitignore" EXCLUDE
)
