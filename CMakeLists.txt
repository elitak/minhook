cmake_minimum_required(VERSION 2.6)
  
project(MinHook)

include (GenerateExportHeader)

set(SRCS
  ./src/buffer.cpp
  ./src/export.cpp
  ./src/hook.cpp
  ./src/thread.cpp
  ./src/trampoline.cpp
)
         
add_library(MyLibrary ${LIB_TYPE} ${SRCS})

GENERATE_EXPORT_HEADER( MyLibrary
  BASE_NAME MyLibrary
  EXPORT_MACRO_NAME MyLibrary_EXPORT
  EXPORT_FILE_NAME MyLibrary_Export.h
  STATIC_DEFINE MyLibrary_BUILT_AS_STATIC
)
