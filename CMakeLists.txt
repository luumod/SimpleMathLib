cmake_minimum_required(VERSION 3.14)
project(MathLib VERSION 1.0.0)

# 定义静态库目标
add_library(${PROJECT_NAME} STATIC src/MathLib.cpp)
message("-----------------PROJECT_NAME: ${PROJECT_NAME}")

# 设置头文件路径
target_include_directories(${PROJECT_NAME} PUBLIC 
    $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include> # 构建时用：<include/MathLib.h>
    $<INSTALL_INTERFACE:include> # 安装后用：include下的所有文件可以直接引用: <MathLib.h>
)

message("------------------CMAKE_SOURCE_DIR: ${CMAKE_SOURCE_DIR}")


# 跨平台安装
include(GNUInstallDirs)

# 安装库文件
install(TARGETS ${PROJECT_NAME} 
    EXPORT MathLibTargets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

# 安装头文件
install(DIRECTORY 
    include/ DESTINATION include
)

# 导出 MathLibTargets.cmake
install(EXPORT MathLibTargets
    FILE MathLibTargets.cmake
    NAMESPACE MathLib::
    DESTINATION ${CMAKE_INSTALL_BINDIR}/cmake/MathLib
)

# 安装 MathLibConfig.cmake
install(FILES 
    cmake/MathLibConfig.cmake DESTINATION ${CMAKE_INSTALL_BINDIR}/cmake/MathLib
)