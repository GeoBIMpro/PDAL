#
# Greyhound plugin CMake configuration
#

add_definitions(-DHAVE_JSONCPP=1)
if (WIN32)
add_definitions("-DARBITER_DLL_IMPORT")
endif()

PDAL_ADD_PLUGIN(libname reader greyhound
    FILES
        io/CompressionStream.cpp
        io/GreyhoundReader.cpp
        io/bounds.cpp
    LINK_WITH ${PDAL_JSONCPP_LIB_NAME})
target_include_directories(${libname} PRIVATE
    ${PDAL_JSONCPP_INCLUDE_DIR}
    ${PDAL_VENDOR_DIR})


if (WITH_TESTS)
    PDAL_ADD_TEST(pdal_io_greyhound_reader_test
        FILES
            test/GreyhoundReaderTest.cpp
        LINK_WITH ${libname} )
target_include_directories(pdal_io_greyhound_reader_test PRIVATE
    ${PDAL_JSONCPP_INCLUDE_DIR}
    ${PDAL_VENDOR_DIR})
endif()
