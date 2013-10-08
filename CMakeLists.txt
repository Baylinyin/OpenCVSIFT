cmake_minimum_required(VERSION 2.8)

#项目名
project(OpenCVSIFT)

#包含include搜索			  
include_directories(${PROJECT_SOURCE_DIR}/include)

#包含OpenCV目录,都build即可.
find_path(OpenCV_PATH OPENCV $ENV{OPENCV_DIR})
message(${OpenCV_PATH})
set(OpencvCV_INC ${OpenCV_PATH}/include)
set(OpencvCV_x64LIB ${OpenCV_PATH}/x64/vc10)
message(${OpencvCV_INC})
message(${OpencvCV_x64LIB})


include_directories(${OpencvCV_INC})
link_directories(${OpencvCV_x64LIB}/lib)

#源文件
file(GLOB lib_srcs src/*.*)
#头文件
file(GLOB lib_hdrs include/*.*)
#单元测试
file(GLOB tool tool/*.*)

#Define a grouping for sources in the makefile.
source_group("INCLUDE" FILES ${lib_hdrs} )
source_group("SOURCE" FILES ${lib_srcs})


#生成静态库
add_library(OpenCVSIFT STATIC ${lib_hdrs} ${lib_srcs})
target_link_libraries(OpenCVSIFT opencv_features2d245d.lib
                                                        opencv_core245d.lib
                                                        opencv_features2d245d.lib
                                                        opencv_highgui245d.lib
                                                        opencv_nonfree245d.lib
                                                        opencv_imgproc245d.lib)

#生成可执行文件			  
add_executable(tools ${tool})
#设置依赖的动态库
target_link_libraries(tools OpenCVSIFT)

