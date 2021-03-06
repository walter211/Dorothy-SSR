cmake_minimum_required(VERSION 3.4.1)

file(GLOB_RECURSE src-files FOLLOW_SYMLINKS *.cpp)

include_directories(
	src/main/cpp/3rdParty/SDL2/Header
	src/main/cpp/3rdParty/BGFX/Header
)

add_library( SDL2-lib SHARED IMPORTED )
set_target_properties(
	SDL2-lib PROPERTIES IMPORTED_LOCATION
	${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/3rdParty/SDL2/Lib/Android/${ANDROID_ABI}/libSDL2.so
)

add_library( BGFX-lib STATIC IMPORTED )
set_target_properties(
	BGFX-lib PROPERTIES IMPORTED_LOCATION
	${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/3rdParty/BGFX/Lib/Android/${ANDROID_ABI}/libbgfx.a
)

add_library( main SHARED ${src-files} )

target_link_libraries( main android log EGL GLESv1_CM GLESv2 SDL2-lib BGFX-lib )
