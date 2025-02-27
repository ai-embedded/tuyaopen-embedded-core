cmake_minimum_required(VERSION 3.10)

project(switch_demo)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CONFIG_ENABLE_WIRED "Enable wired" ON)

set(TUYAOPEN_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../..)
set(SRCS 
    "main.c"
    "qrencode_print.c"
)

list(APPEND SRCS 
    "libqrencode/qrencode.c"
    "libqrencode/qrinput.c"
    "libqrencode/bitstream.c"
    "libqrencode/qrspec.c"
    "libqrencode/rsecc.c"
    "libqrencode/split.c"
    "libqrencode/mask.c"
    "libqrencode/mqrspec.c"
    "libqrencode/mmask.c"
)

add_executable(${PROJECT_NAME} 
    ${SRCS}
)

target_include_directories(${PROJECT_NAME} PUBLIC . "libqrencode")

add_definitions(-DSTATIC_IN_RELEASE=static)
add_definitions(-DMAJOR_VERSION=4 -DMINOR_VERSION=1 -DMICRO_VERSION=1 -DVERSION=\"4.1.1\")

set(COMPONENT_LIBS "")

add_subdirectory(${TUYAOPEN_ROOT_DIR}/components ${CMAKE_CURRENT_BINARY_DIR}/components_build)
add_subdirectory(${TUYAOPEN_ROOT_DIR}/port ${CMAKE_CURRENT_BINARY_DIR}/port_build)

# 链接所有启用的组件到主程序
foreach(COMPONENT IN LISTS COMPONENT_LIBS)
    target_link_libraries(${PROJECT_NAME} PRIVATE ${COMPONENT})
endforeach()
