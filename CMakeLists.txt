cmake_minimum_required(VERSION 3.22)
project(FFplay_debug C)

set(CMAKE_C_STANDARD 99)

# FFmpeg的安装目录，可以通过命令"brew info ffmpeg"获取
# 需要替换成自己的FFMpeg安装目录
set(FFMPEG_DIR /opt/homebrew/Cellar/ffmpeg/5.0.1)

# SDL2的安装目录，可以通过命令"brew info sdl2"获取
# 需要替换成自己的SDL2安装目录
set(SDL2_DIR /opt/homebrew/Cellar/sdl2/2.0.20)

# 头文件搜索路径
include_directories(${FFMPEG_DIR}/include/)

include_directories(${CMAKE_SOURCE_DIR})

include_directories(${SDL2_DIR}/include/SDL2/)

# 动态链接库或静态链接库的搜索路径
link_directories(${FFMPEG_DIR}/lib/)

link_directories(${SDL2_DIR}/lib/)

#将指定文件设置在FFmpeg_debug_source变量中
file(GLOB FFplay_debug_source ${CMAKE_SOURCE_DIR}/*.*)

add_executable(FFplay_debug ${FFplay_debug_source})

#链接库
target_link_libraries(FFplay_debug
        #FFmpeg 库
        avcodec
        avdevice
        postproc
        avfilter
        avformat
        avutil
        swresample
        swscale
        # SDL2库
        SDL2
        )