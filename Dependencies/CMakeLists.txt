add_library(glad-gl3-iplug "IGraphics/glad_GL3/src/glad.c")
target_include_directories(glad-gl3-iplug PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/glad_GL3/include")

add_library(nanosvg-iplug INTERFACE)
target_include_directories(nanosvg-iplug INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/NanoSVG/src")

add_library(nanovg-iplug "IGraphics/NanoVG/src/nanovg.c")
target_include_directories(nanovg-iplug PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/NanoVG/src")

add_library(stb-iplug INTERFACE)
target_include_directories(stb-iplug INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/STB")

# We define our own VST3 dependencies
set(VST3_BASE_DIR ${IPLUG_VST3_SDK_PATH}/base)
set(VST3_PLUGINTERFACES_DIR ${IPLUG_VST3_SDK_PATH}/pluginterfaces)
set(VST3_PUBLIC_SDK_DIR ${IPLUG_VST3_SDK_PATH}/public.sdk)
add_library(iplug-vst3core
  ${VST3_BASE_DIR}/source/baseiids.cpp
  ${VST3_BASE_DIR}/source/classfactoryhelpers.h
  ${VST3_BASE_DIR}/source/fbuffer.cpp
  ${VST3_BASE_DIR}/source/fbuffer.h
  ${VST3_BASE_DIR}/source/fcleanup.h
  ${VST3_BASE_DIR}/source/fcommandline.h
  ${VST3_BASE_DIR}/source/fdebug.cpp
  ${VST3_BASE_DIR}/source/fdebug.h
  ${VST3_BASE_DIR}/source/fdynlib.cpp
  ${VST3_BASE_DIR}/source/fdynlib.h
  ${VST3_BASE_DIR}/source/fobject.cpp
  ${VST3_BASE_DIR}/source/fobject.h
  ${VST3_BASE_DIR}/source/fstdmethods.h
  ${VST3_BASE_DIR}/source/fstreamer.cpp
  ${VST3_BASE_DIR}/source/fstreamer.h
  ${VST3_BASE_DIR}/source/fstring.cpp
  ${VST3_BASE_DIR}/source/fstring.h
  ${VST3_BASE_DIR}/source/hexbinary.h
  ${VST3_BASE_DIR}/source/timer.cpp
  ${VST3_BASE_DIR}/source/timer.h
  ${VST3_BASE_DIR}/source/updatehandler.cpp
  ${VST3_BASE_DIR}/source/updatehandler.h

  ${VST3_BASE_DIR}/thread/source/fcondition.cpp
  ${VST3_BASE_DIR}/thread/source/flock.cpp

  ${VST3_PLUGINTERFACES_DIR}/base/conststringtable.cpp
  ${VST3_PLUGINTERFACES_DIR}/base/conststringtable.h
  ${VST3_PLUGINTERFACES_DIR}/base/coreiids.cpp
  ${VST3_PLUGINTERFACES_DIR}/base/funknown.cpp
  ${VST3_PLUGINTERFACES_DIR}/base/funknown.h
  ${VST3_PLUGINTERFACES_DIR}/base/ustring.cpp
  ${VST3_PLUGINTERFACES_DIR}/base/ustring.h

  ${VST3_PUBLIC_SDK_DIR}/source/common/memorystream.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/common/memorystream.h
  ${VST3_PUBLIC_SDK_DIR}/source/common/pluginview.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/common/pluginview.h
  ${VST3_PUBLIC_SDK_DIR}/source/common/commoniids.cpp

  ${VST3_PUBLIC_SDK_DIR}/source/main/dllmain.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/main/pluginfactory.cpp

  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstaudioeffect.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstaudioeffect.h
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstbus.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstbus.h
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstcomponent.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstcomponent.h
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstcomponentbase.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstcomponentbase.h
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstinitiids.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstparameters.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstparameters.h
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstsinglecomponenteffect.cpp
  ${VST3_PUBLIC_SDK_DIR}/source/vst/vstsinglecomponenteffect.h
)
target_include_directories(iplug-vst3core PUBLIC ${IPLUG_VST3_SDK_PATH})