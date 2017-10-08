cmake_minimum_required(VERSION 2.8)

set(AD3_SRC_FILES
  ad3/FactorGraph.cpp
  ad3/GenericFactor.cpp
  ad3/Factor.cpp
  ad3/Utils.cpp
)

option(REMOVE_SOME_WARNINGS "Remove some annoying warnings from eigen" ON)

   

# remove some warnings from Eigen
if(REMOVE_SOME_WARNINGS AND (CMAKE_CXX_COMPILER_ID MATCHES "GNU" OR CMAKE_CXX_COMPILER_ID MATCHES "Clang"))
    add_definitions(-Wno-ignored-attributes)
    add_definitions(-Wno-deprecated-declarations)
endif()



include_directories( ad3 )
#include_directories( Eigen )



ADD_LIBRARY(ad3 SHARED ${AD3_SRC_FILES})



install(TARGETS ad3
    RUNTIME DESTINATION bin         COMPONENT libraries
    LIBRARY DESTINATION lib         COMPONENT libraries
    ARCHIVE DESTINATION lib/static  COMPONENT libraries)


install (TARGETS ad3
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin)




install(DIRECTORY ad3
    DESTINATION include
    FILES_MATCHING
    PATTERN "*.h"
    PATTERN ".svn" EXCLUDE
)
