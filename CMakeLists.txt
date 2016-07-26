project ( toluapp C )
cmake_minimum_required ( VERSION 2.8 )

include_directories ( include src/lib ${Lua_INCLUDE_DIR} )

# Build lib
file ( GLOB SRC_LIBTOLUAPP src/lib/*.c )
if ( MSVC )
  set ( DEF_FILE libtoluapp.def )
endif ( )

add_library ( toluapp_lib ${SRC_LIBTOLUAPP} ${DEF_FILE} )
target_link_libraries ( toluapp_lib Lua )
set_target_properties ( toluapp_lib PROPERTIES OUTPUT_NAME toluapp CLEAN_DIRECT_OUTPUT 
  1 )

# Build app
include_directories ( src/bin )
set ( SRC_TOLUA src/bin/tolua.c src/bin/toluabind.c )
add_executable ( toluapp ${SRC_TOLUA} )
target_link_libraries ( toluapp Lua toluapp_lib )
