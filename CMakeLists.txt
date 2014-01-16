cmake_minimum_required(VERSION 2.6)
  
project(libMinHook)

include (GenerateExportHeader)

include_directories ("./include")

# TODO put this here or leave it as a conditional in trampoline.cpp?
#if(CHOST MATCHES ".*64.*")
#  include_directories ("./src/hde64")
#else()
#  include_directories ("./src/hde32")
#endif()


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
         
add_library(MinHook ${LIB_TYPE} ${SRCS})

GENERATE_EXPORT_HEADER( MinHook
  BASE_NAME MinHook
  EXPORT_MACRO_NAME MyLibrary_EXPORT
  EXPORT_FILE_NAME MinHook.h
  STATIC_DEFINE MyLibrary_BUILT_AS_STATIC
)

# FIXME set in toolchain?
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D _WIN32_WINNT=0x0501")
