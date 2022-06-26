cmake_minimum_required(VERSION 3.2 FATAL_ERROR)
project(SexyPsf VERSION 0.4.8 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set (CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH}" "${CMAKE_CURRENT_LIST_DIR}/cmake")

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_LIST_DIR})
include_directories(${CMAKE_CURRENT_LIST_DIR}/3rdParty/miniz)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/3rdParty/miniz)


add_executable(SexyPsf 
    spu/adsr.c
    spu/adsr.h
    spu/dma.c
    spu/dma.h
    spu/externals.h
    spu/gauss_i.h
    spu/registers.c
    spu/registers.h
    spu/regs.h
    spu/reverb.c
    spu/spu.c
    spu/spu.h
    spu/stdafx.h
    Misc.c
    PsxBios.c
    PsxCounters.c
    PsxDma.c
    PsxHLE.c
    PsxHw.c
    PsxInterpreter.c
    PsxMem.c
    R3000A.c
    Spu.c
    Linux/oss.h
    Linux/oss.c
    Linux/Linux.h
    Linux/LnxMain.c)


target_compile_definitions(SexyPsf PRIVATE "_CRT_SECURE_NO_WARNINGS")
target_link_libraries(SexyPsf ${SDL2_LIBRARIES} miniz)
export(TARGETS SexyPsf FILE SexyPsf.cmake)

if (MSVC)
    # /WX
    target_compile_options(SexyPsf PRIVATE /W4 /wd4996 /MP)
endif()
