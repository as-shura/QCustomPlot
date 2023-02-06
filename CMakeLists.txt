cmake_minimum_required(VERSION 3.8.2)

project(qcustomplot)

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

target_include_directories(qcustomplot PUBLIC include)
# Add the Qt5 Widgets for linking
target_link_libraries(qcustomplot Qt5::Core Qt5::Gui Qt5::Widgets)