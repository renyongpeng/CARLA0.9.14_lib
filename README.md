CMakeList文件内容：
请把下面的内容合理的添加到你的CmakeList.txt当中去：

cmake_minimum_required(VERSION 3.26)
project(test)

set(CMAKE_CXX_STANDARD 14)

# 记得改成自己的路径
set(CARLA_LIB "$ENV{HOME}/xxx/carla/carla_lib")  

add_executable(${PROJECT_NAME}
        main.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE ${CARLA_LIB}/include)

target_link_directories(${PROJECT_NAME} PRIVATE ${CARLA_LIB}/lib)

target_compile_options(${PROJECT_NAME} PRIVATE -isystem ${CARLA_LIB}/include/system)

target_link_libraries(${PROJECT_NAME} PRIVATE
        -Wl,-Bstatic -lcarla_client -lrpc -lboost_filesystem -Wl,-Bdynamic
        -lpng
        -ltiff
        -ljpeg
        -lRecast
        -lDetour
        -lDetourCrowd -pthread)

