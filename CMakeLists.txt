cmake_minimum_required(VERSION 2.6)
  
project(libMinHook)

include (GenerateExportHeader)

include_directories ("./include")

# TODO wrap this in linux detect and add notes, or is that improper/impossible? 
#set(CMAKE_TOOLCHAIN_FILE "./Toolchain-i686-mingw32.cmake")

# TODO use globbing?
set(SRCS
  ./src/buffer.cpp
  ./src/export.cpp
  ./src/hook.cpp
  ./src/thread.cpp
  ./src/trampoline.cpp
)

# TODO I'm not yet fully abstracting these includes since trampoline.cpp has a lot
# of ifdef _M_X64 directives in it
include_directories ("./src/hde")
if(CMAKE_CXX_COMPILER MATCHES "64")
  list(APPEND SRCS ./src/hde/hde64.c)
else()
  list(APPEND SRCS ./src/hde/hde32.c)
endif()
         
set(LIB_TYPE SHARED)
add_library(MinHook ${LIB_TYPE} ${SRCS})

GENERATE_EXPORT_HEADER( MinHook
  BASE_NAME MinHook
  EXPORT_MACRO_NAME MyLibrary_EXPORT
  EXPORT_FILE_NAME MinHook.h
  STATIC_DEFINE MyLibrary_BUILT_AS_STATIC
)

# FIXME set in toolchain?
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D _WIN32_WINNT=0x0501")
