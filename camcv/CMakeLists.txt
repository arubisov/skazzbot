cmake_minimum_required(VERSION 2.8)
project(camcv_vid1)
SET(COMPILE_DEFINITIONS -Werror)

#OPENCV
find_package(OpenCV REQUIRED)
#except if you’re pierre, change the folder where you installed libfacerec
#optional, only if you want to go till step 6 : face recognition
link_directories(/home/pi/camcv/libfacerec-0.04) 

include_directories(/opt/vc/userland/host_applications/linux/libs/bcm_host/include)
include_directories(/opt/vc/userland/host_applications/linux/apps/raspicam/gl_scenes)
include_directories(/opt/vc/userland/interface/vcos)
include_directories(/opt/vc/userland)
include_directories(/opt/vc/userland/interface/vcos/pthreads)
include_directories(/opt/vc/userland/interface/vmcs_host/linux)
include_directories(/opt/vc/userland/interface/khronos/include)
include_directories(/opt/vc/userland/interface/khronos/common)
add_executable(camcv_vid1 RaspiCamControl.c RaspiCLI.c RaspiPreview.c camcv_vid1.cpp RaspiTex.c RaspiTexUtil.c tga.c gl_scenes/teapot.c gl_scenes/models.c gl_scenes/square.c gl_scenes/mirror.c gl_scenes/yuv.c gl_scenes/sobel.c)
target_link_libraries(camcv_vid1 /opt/vc/lib/libmmal_core.so /opt/vc/lib/libmmal_util.so /opt/vc/lib/libmmal_vc_client.so /opt/vc/lib/libvcos.so /opt/vc/lib/libbcm_host.so /opt/vc/lib/libGLESv2.so /opt/vc/lib/libEGL.so /home/pi/camcv/libfacerec-0.04/libopencv_facerec.a ${OpenCV_LIBS})
