cmake_minimum_required(VERSION 3.5)

project(ukncbtl 
  LANGUAGES CXX 
  VERSION 1.0.599.0
)

set(CMAKE_RC_FLAGS "--use-temp-file")

set(PROJECT_HEADERS_DIR src/ukncbtl/emulator)
set(PROJECT_HEADERS
  ${PROJECT_HEADERS_DIR}/emubase/Board.h
  ${PROJECT_HEADERS_DIR}/emubase/Defines.h
  ${PROJECT_HEADERS_DIR}/emubase/Emubase.h
  ${PROJECT_HEADERS_DIR}/emubase/Processor.h

  ${PROJECT_HEADERS_DIR}/util/BitmapFile.h
  ${PROJECT_HEADERS_DIR}/util/WavPcmFile.h

  ${PROJECT_HEADERS_DIR}/Common.h
  ${PROJECT_HEADERS_DIR}/Dialogs.h
  ${PROJECT_HEADERS_DIR}/Emulator.h
  ${PROJECT_HEADERS_DIR}/Main.h
  ${PROJECT_HEADERS_DIR}/SoundGen.h
  ${PROJECT_HEADERS_DIR}/ToolWindow.h
  ${PROJECT_HEADERS_DIR}/Views.h
)

set(PROJECT_SOURCES_DIR src/ukncbtl/emulator)
set(PROJECT_SOURCES
  ${PROJECT_SOURCES_DIR}/emubase/Board.cpp
  ${PROJECT_SOURCES_DIR}/emubase/Disasm.cpp
  ${PROJECT_SOURCES_DIR}/emubase/Floppy.cpp
  ${PROJECT_SOURCES_DIR}/emubase/Hard.cpp
  ${PROJECT_SOURCES_DIR}/emubase/Memory.cpp
  ${PROJECT_SOURCES_DIR}/emubase/Processor.cpp

  ${PROJECT_SOURCES_DIR}/util/BitmapFile.cpp
  ${PROJECT_SOURCES_DIR}/util/WavPcmFile.cpp

  ${PROJECT_SOURCES_DIR}/Common.cpp
  ${PROJECT_SOURCES_DIR}/ConsoleView.cpp
  ${PROJECT_SOURCES_DIR}/DebugView.cpp
  ${PROJECT_SOURCES_DIR}/Dialogs.cpp
  ${PROJECT_SOURCES_DIR}/DisasmView.cpp
  ${PROJECT_SOURCES_DIR}/Emulator.cpp
  ${PROJECT_SOURCES_DIR}/KeyboardView.cpp
  ${PROJECT_SOURCES_DIR}/Main.cpp
  ${PROJECT_SOURCES_DIR}/MainWindow.cpp
  ${PROJECT_SOURCES_DIR}/MemoryView.cpp
  ${PROJECT_SOURCES_DIR}/ScreenView.cpp
  ${PROJECT_SOURCES_DIR}/Settings.cpp
  ${PROJECT_SOURCES_DIR}/SoundGen.cpp
  ${PROJECT_SOURCES_DIR}/SpriteView.cpp
  ${PROJECT_SOURCES_DIR}/TapeView.cpp
  ${PROJECT_SOURCES_DIR}/ToolWindow.cpp

  # i don't know how to force CMake use *.xml as *.manifest, see workaround below
  #${PROJECT_SOURCES_DIR}/manifest.xml

  ${PROJECT_SOURCES_DIR}/res/UKNCBTL.rc
)

# WORKAROUND: how to force cmake use .xml as .manifest?
configure_file(
  ${PROJECT_SOURCES_DIR}/manifest.xml ${PROJECT_NAME}.manifest
  COPYONLY
)

add_executable(${PROJECT_NAME}
  ${PROJECT_HEADERS}
  ${PROJECT_SOURCES}
  ${PROJECT_NAME}.manifest
)

target_include_directories(${PROJECT_NAME}
  PRIVATE ${PROJECT_HEADERS_DIR}
)

#target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Wconversion -Wsign-conversion)
target_link_options(${PROJECT_NAME}
  PRIVATE "-municode"
)

set_target_properties(${PROJECT_NAME} 
  PROPERTIES WIN32_EXECUTABLE 1
)

target_link_libraries(${PROJECT_NAME} 
  PRIVATE comctl32.lib winmm.lib vfw32.lib
)
