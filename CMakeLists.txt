cmake_minimum_required(VERSION "3.10.0")

project(rtl_fm_sdlplayer C)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

find_package(Threads)
find_package(PkgConfig)
find_package(SDL2)

if(MINGW)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mconsole -s")
endif(MINGW)


if(PKG_CONFIG_FOUND)
    pkg_check_modules(LIBUSB libusb-1.0 IMPORTED_TARGET)
else()
    set(LIBUSB_LIBRARIES "" CACHE STRING "manual libusb path")
    set(LIBUSB_INCLUDE_DIRS "" CACHE STRING "manual libusb includepath")
endif()

if (NOT SDL2_FOUND)
    message(FATAL_ERROR "SDL2 required to compile rtl_fm_sdlplayer!")
endif ()

if(UNIX)
    set(DETACH_KERNEL_DRIVER ON CACHE BOOL "kernel driver detaching enabled")
endif(UNIX)

set(LINK_RTL_APPS_WITH_STATIC_LIB ON CACHE BOOL "Static link rtl-apps with librtlsdr")

add_subdirectory(rtl-sdr)

include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/rtl-sdr/include
    ${CMAKE_CURRENT_SOURCE_DIR}/rtl-sdr/src
    ${SDL2_INCLUDE_DIRS}
    ${LIBUSB_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME}
    src/rtl_fm_player.c src/rtl_fm_player.h
)

target_link_libraries(${PROJECT_NAME}
    rtlsdr_static
    convenience_static
    ${SDL2_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    ${LIBUSB_LIBRARIES}
)

if(MINGW)
    target_link_libraries(${PROJECT_NAME} imm32 winmm version setupapi hid hidapi samplerate)
endif(MINGW)
