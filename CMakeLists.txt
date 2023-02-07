cmake_minimum_required(VERSION 3.8.2)

project(qcustomplot VERSION 1.0.0)

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Turn on automatic invocation of the MOC, UIC & RCC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# There may be a way to tell up front if Qt5 is going to be found, but I haven't found
# a foolproof way to do it yet, so settle for the default error message for now.
#if(NOT CMAKE_PREFIX_PATH AND NOT Qt5Widgets_DIR)
#    message(WARNING "CMAKE_PREFIX_PATH is not defined, so find_package may not work. Set the CMAKE_PREFIX_PATH "
#            "environment variable to the install prefix of Qt 5, either on the command line as "
#            "-DCMAKE_PREFIX_PATH=\"path/to/Qt5/lib/cmake\" or with set(CMAKE_PREFIX_PATH path/to/Qt5/lib/cmake)")
#endif(NOT CMAKE_PREFIX_PATH AND NOT Qt5Widgets_DIR)

# Add a compiler flag
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

# Find the QtWidgets library
find_package(Qt5 REQUIRED COMPONENTS Core Gui Widgets)

set(HEADERS
    include/qcustomplot.h
)

set(SRCS
    src/qcustomplot.cpp
)

# Tell CMake to create the helloworld executable
add_library(qcustomplot ${SRCS} ${HEADERS})

include_directories(include)
# Add the Qt5 Widgets for linking
target_link_libraries(qcustomplot Qt5::Core Qt5::Gui Qt5::Widgets)

export(TARGETS qcustomplot NAMESPACE qcustomplot:: FILE qcustomplotTargets.cmake)

install(TARGETS qcustomplot
    EXPORT qcustomplotTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

install(FILES ${HEADER} DESTINATION include)

install(DIRECTORY include/
        DESTINATION include/)
        
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    qcustomplotConfigVersion.cmake
    VERSION ${PACKAGE_VERSION}
    COMPATIBILITY AnyNewerVersion
)

install(EXPORT qcustomplotTargets
        FILE qcustomplotTargets.cmake
        NAMESPACE qcustomplot::
        DESTINATION lib/cmake/qcustomplot
)

configure_file(qcustomplotConfig.cmake.in qcustomplotConfig.cmake @ONLY)