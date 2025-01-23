# SimpleMathLib

## Linux系统
### 编译
在项目根目录下运行以下命令：
1. `cmake -S . -B build`
2. `cd build && make -j && sudo cmake --install -build --prefix /usr/lib/install`
### 使用
新建一个项目：至少具有CMakeLists.txt与一个main.cpp
其中CMakeLists.txt的内容：
```cmake
cmake_minimum_required(VERSION 3.10)

project(MyApp)

list(APPEND CMAKE_PREFIX_PATH "/usr/lib/install") # 重要

find_package(MathLib REQUIRED)

add_executable(MyApp main.cpp)

target_link_libraries(MyApp PRIVATE MathLib::MathLib)
```

## Windows系统（MSVC）
### 编译
在项目根目录下运行以下命令：
1. `cmake -S . -B build`
2. `cd build`
3. `start MathLib.sln`
4. `生成`--> `生成解决方案`
5. 在build的Debug文件夹下就生成了MathLib.lib
### 使用
新建一个项目：至少具有CMakeLists.txt与一个main.cpp
其中CMakeLists.txt的内容：
```cmake
cmake_minimum_required(VERSION 3.10)

project(AnotherProject)

set(MATHLIB_DIR "F:/code/SimpleMathLib/build/Debug") # 库文件位置

set(SOURCES main.cpp)

add_executable(AnotherProject ${SOURCES}) 

include_directories("F:/code/SimpleMathLib/include") # 头文件位置

target_link_libraries(AnotherProject "${MATHLIB_DIR}/MathLib.lib")


```
