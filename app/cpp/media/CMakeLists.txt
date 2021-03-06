add_subdirectory(ffmpeg_run)

set(FFMPEG_DIR ffmepg_install)

#当前目录下的使用相对路径
INCLUDE_DIRECTORIES(${FFMPEG_DIR}/${ANDROID_ABI}/include ../common ..)

add_library(avcodec SHARED IMPORTED)
set_target_properties(avcodec
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libavcodec.so)

add_library(avdevice SHARED IMPORTED)
set_target_properties(avdevice
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libavdevice.so)

add_library(avfilter SHARED IMPORTED)
set_target_properties(avfilter
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libavfilter.so)

add_library(avformat SHARED IMPORTED)
set_target_properties(avformat
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libavformat.so)

add_library(avutil SHARED IMPORTED)
set_target_properties(avutil PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libavutil.so)

add_library(postproc SHARED IMPORTED)
set_target_properties(postproc
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libpostproc.so)

add_library(swresample SHARED IMPORTED)
set_target_properties(swresample
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libswresample.so)

add_library(swscale SHARED IMPORTED)
set_target_properties(swscale
        PROPERTIES IMPORTED_LOCATION
        ${PROJECT_SOURCE_DIR}/../libs/${ANDROID_ABI}/libswscale.so)



SET(FFMPEGTOOL_LIBS avutil
                    avdevice
                    avcodec
                    swresample
                    swscale
                    postproc
                    avformat
                    avfilter
                    android
                    log
                    ffmpeg)

SET(FFMPEGTOOL_LIB_SRCS ffmpeg_version.cpp
        merge.cpp
        hw_decode_video.cpp
        codecimpl.cpp
        yuv420p_util.cpp
        ffmpeg_tool_impl.cpp
        ffmepg_cmd_impl.cpp
        jni_load.cpp)
ADD_LIBRARY(ffmpegtool SHARED ${FFMPEGTOOL_LIB_SRCS})
TARGET_LINK_LIBRARIES(ffmpegtool ${FFMPEGTOOL_LIBS})
