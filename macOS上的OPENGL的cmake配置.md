# CMakeLists.txt的内容和解释  

```CMake

cmake_minimum_required(VERSION 3.0.0)
project(my_cmake)
set(CMAKE_CXX_STANDARD 17)
set(ENV{PKG_CONFIG_PATH} /usr/local/opt/libffi/lib/pkgconfig)
find_package(PkgConfig)
pkg_search_module(GTKMM3 REQUIRED gtkmm-3.0)
pkg_search_module(GLEW REQUIRED glew)
pkg_search_module(GLM REQUIRED glm)
add_executable(my_cmake
        main.cpp
        fileReader.cpp
        shaderUtil.cpp
        MainWindow.cpp
        stage.cpp
        )

target_include_directories(my_cmake
        PRIVATE ${GTKMM3_INCLUDE_DIRS}
        PRIVATE ${GLEW_INCLUDE_DIRS}
        PRIVATE ${GLM_INCLUDE_DIRS}
        PRIVATE include
        )
target_link_directories(my_cmake
        PRIVATE ${GTKMM3_LIBRARY_DIRS}
        PRIVATE ${GLEW_LIBRARY_DIRS}
        )
target_link_libraries(my_cmake
        ${GTKMM3_LIBRARIES}
        ${GLEW_LIBRARIES}
        "-framework OpenGL"
        )

add_executable(test
        test.cpp test.cpp)
```
链接OPENGL库需要 `"-framework OpenGL"`
如果是在Windows平台下，这一行应改为 `opengl32`
