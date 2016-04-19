cmake_minimum_required(VERSION 3.3)

include_directories(. ../core ../posix ../lib)
link_directories(. ../core ../posix ../lib)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -lpthread -v")
set(CMAKE_BUILD_TYPE Debug)
add_definitions(-DPUBNUB_CALLBACK_API) # -DPUBNUB_THREADSAFE) # threadsafe definition was causing problems

set(SOURCE_FILES ../core/pubnub_coreapi.c ../core/pubnub_coreapi.h ../core/pubnub_ccore.c ../core/pubnub_ccore.h ../core/pubnub_netcore.c ../core/pubnub_netcore.h ../lib/sockets/pbpal_sockets.c ../lib/sockets/pbpal_resolv_and_connect_sockets.c ../core/pubnub_alloc_std.c ../core/pubnub_assert_std.c ../core/pubnub_generate_uuid.c ../core/pubnub_generate_uuid.h ../core/pubnub_blocking_io.c ../core/pubnub_blocking_io.h ../core/pubnub_timers.c ../core/pubnub_timers.h ../core/pubnub_json_parse.c ../core/pubnub_json_parse.h ../core/pubnub_helper.c ../core/pubnub_helper.h ../posix/pubnub_version_posix.c ../posix/pubnub_generate_uuid_posix.c ../posix/pbpal_posix_blocking_io.c ../core/pubnub_timer_list.c ../core/pubnub_timer_list.h ../posix/pubnub_ntf_callback_posix.c ../posix/pubnub_get_native_socket.c ../posix/pubnub_get_native_socket.h pubnub_futres_cpp11.cpp)

if(APPLE)
        set(SOURCE_FILES ${SOURCE_FILES} ../posix/monotonic_clock_get_time_darwin.c)
else(UNIX)
        set(SOURCE_FILES ${SOURCE_FILES} ../posix/monotonic_clock_get_time_posix.c)
        # set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} -lrt)
endif()

add_library(pubnub ${SOURCE_FILES}) ## ../core/pubnub_coreapi.c ../core/pubnub_ccore.c ../core/pubnub_netcore.c  ../lib/sockets/pbpal_sockets.c ../lib/sockets/pbpal_resolv_and_connect_sockets.c ../core/pubnub_alloc_std.c ../core/pubnub_assert_std.c ../core/pubnub_generate_uuid.c ../core/pubnub_blocking_io.c  ../core/pubnub_timers.c ../core/pubnub_json_parse.c ../core/pubnub_helper.c  ../posix/pubnub_version_posix.c ../posix/pubnub_generate_uuid_posix.c ../posix/pbpal_posix_blocking_io.c ../posix/monotonic_clock_get_time_darwin.c ../core/pubnub_timer_list.c ../posix/pubnub_ntf_callback_posix.c ../posix/pubnub_get_native_socket.c pubnub_futres_cpp11.cpp)
