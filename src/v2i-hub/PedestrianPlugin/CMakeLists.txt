PROJECT ( PedestrianPlugin VERSION 3.0.0 LANGUAGES CXX )

SET (TMX_PLUGIN_NAME "Pedestrian")

FIND_PACKAGE (XercesC REQUIRED)
FIND_PACKAGE (NetSNMP REQUIRED)

find_library(libasn1c .)

BuildTmxPlugin ()

TARGET_INCLUDE_DIRECTORIES ( ${PROJECT_NAME} PUBLIC ${XercesC_INCLUDE_DIRS} ${NETSNMP_INCLUDE_DIRS})
TARGET_LINK_LIBRARIES ( ${PROJECT_NAME} tmxutils ${XercesC_LIBRARY} ${NETSNMP_LIBRARIES})

# Locate GTest
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

set(runTests_sources
                test/PedestrianTest.cpp 
                test/Main.cpp
)

# Link runTests with what we want to test and the GTest and pthread library
add_executable(runPedestrianTest ${runTests_sources})

target_link_libraries(runPedestrianTest ${GTEST_LIBRARIES} pthread)