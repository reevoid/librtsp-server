cmake_minimum_required(VERSION 3.10)
project(rtsp VERSION 1.0.0 LANGUAGES C)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(RTSP_SOURCES
    md5.c
    rtp_enc.c
    rtsp_demo.c
    rtsp_msg.c
    stream_queue.c
    utils.c
)

set(RTSP_HEADERS
    rtsp_demo.h
)

add_library(rtsp SHARED ${RTSP_SOURCES})

target_compile_options(rtsp PRIVATE -Wall -Wextra -fPIC)

target_include_directories(rtsp
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include>
)

set_target_properties(rtsp PROPERTIES
    VERSION   ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER "${RTSP_HEADERS}"
)

include(GNUInstallDirs)

install(TARGETS rtsp
    LIBRARY       DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
