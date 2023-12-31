cmake_minimum_required(VERSION 3.16)
project(ch340g)

set(CMAKE_CXX_STANDARD 11)

# Add the source files
set(SOURCES
    ch340g.cpp
    ch340g.h
)

# create shared library
add_library(ch340g SHARED ${SOURCES})
set_target_properties(ch340g PROPERTIES VERSION 0.0.1)
# create static library
add_library(ch340g_static STATIC ${SOURCES})

target_link_directories(
    ch340g
    PUBLIC
    "/lib/x86_64-linux-gnu")

target_link_directories(
    ch340g_static
    PUBLIC
    "/lib/x86_64-linux-gnu")

# Link against libusb
target_link_libraries(ch340g PUBLIC -lusb-1.0)
target_link_libraries(ch340g_static PUBLIC -lusb-1.0)


# Install shared library
install(TARGETS ch340g
        LIBRARY DESTINATION /usr/local/lib
        PERMISSIONS OWNER_READ OWNER_WRITE GROUP_READ WORLD_READ)

# Install static library
install(TARGETS ch340g_static
        ARCHIVE DESTINATION /usr/local/lib
        PERMISSIONS OWNER_READ OWNER_WRITE GROUP_READ WORLD_READ)

# Install header files
install(FILES ch340g.h DESTINATION /usr/local/include)

# Include the tests directory
add_subdirectory(tests)
