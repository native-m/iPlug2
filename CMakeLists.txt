cmake_minimum_required(VERSION 3.20)

project(IPlug2)

option(IPLUG_VST3_SDK_PATH "VST3 SDK Path")
option(IPLUG_BUILD_EXAMPLES "Build examples" ON)
set(IPLUG_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}")

add_subdirectory(Dependencies)
add_subdirectory(WDL)

if (MSVC)
  add_compile_options(/wd4068)
endif ()

set(IPLUG_SOURCE
  "IGraphics/Controls/IBubbleControl.h"
  "IGraphics/Controls/IColorPickerControl.h"
  "IGraphics/Controls/IControls.cpp"
  "IGraphics/Controls/IControls.h"
  "IGraphics/Controls/ICornerResizerControl.h"
  "IGraphics/Controls/IFPSDisplayControl.h"
  "IGraphics/Controls/ILEDControl.h"
  "IGraphics/Controls/IPopupMenuControl.cpp"
  "IGraphics/Controls/IPopupMenuControl.h"
  "IGraphics/Controls/IRTTextControl.h"
  "IGraphics/Controls/IShaderControl.h"
  "IGraphics/Controls/ITextEntryControl.cpp"
  "IGraphics/Controls/ITextEntryControl.h"
  "IGraphics/Controls/IVDisplayControl.h"
  "IGraphics/Controls/IVKeyboardControl.h"
  "IGraphics/Controls/IVMeterControl.h"
  "IGraphics/Controls/IVMultiSliderControl.h"
  "IGraphics/Controls/IVNumberBoxControl.h"
  "IGraphics/Controls/IVPresetManagerControl.h"
  "IGraphics/Controls/IVScopeControl.h"
  "IGraphics/Controls/IWebViewControl.h"

  "IGraphics/Extras/IGraphicsFlexBox.cpp"
  "IGraphics/Extras/IGraphicsFlexBox.h"

  "IGraphics/IControl.cpp"
  "IGraphics/IControl.h"
  "IGraphics/IGraphics.cpp"
  "IGraphics/IGraphics.h"
  "IGraphics/IGraphicsConstants.h"
  "IGraphics/IGraphicsEditorDelegate.cpp"
  "IGraphics/IGraphicsEditorDelegate.h"
  "IGraphics/IGraphicsLiveEdit.h"
  "IGraphics/IGraphicsPopupMenu.h"
  "IGraphics/IGraphicsPrivate.h"
  "IGraphics/IGraphicsStructs.h"
  "IGraphics/IGraphicsUtilities.h"
  "IGraphics/IGraphics_include_in_plug_hdr.h"
  "IGraphics/IGraphics_include_in_plug_src.h"
  "IGraphics/IGraphics_select.h"

  "IPlug/Extras/HIIR/FPUDownsampler2x.h"
  "IPlug/Extras/HIIR/FPUStageProc.h"
  "IPlug/Extras/HIIR/FPUUpsampler2x.h"
  "IPlug/Extras/HIIR/PolyphaseIIR2Designer.cpp"
  "IPlug/Extras/HIIR/PolyphaseIIR2Designer.h"

  "IPlug/Extras/OSC/IPlugOSC.cpp"
  "IPlug/Extras/OSC/IPlugOSC.h"
  "IPlug/Extras/OSC/IPlugOSC_msg.cpp"
  "IPlug/Extras/OSC/IPlugOSC_msg.h"

  "IPlug/Extras/Synth/ControlRamp.h"
  "IPlug/Extras/Synth/MidiSynth.cpp"
  "IPlug/Extras/Synth/MidiSynth.h"
  "IPlug/Extras/Synth/SynthVoice.h"
  "IPlug/Extras/Synth/VoiceAllocator.cpp"
  "IPlug/Extras/Synth/VoiceAllocator.h"

  "IPlug/Extras/ADSREnvelope.h"
  "IPlug/Extras/Easing.h"
  "IPlug/Extras/LFO.h"
  "IPlug/Extras/NChanDelay.h"
  "IPlug/Extras/Oscillator.h"
  "IPlug/Extras/Oscillator_table.h"
  "IPlug/Extras/Oversampler.h"
  "IPlug/Extras/Smoothers.h"
  "IPlug/Extras/SVF.h"

  "IPlug/IPlugAPIBase.cpp"
  "IPlug/IPlugAPIBase.h"
  "IPlug/IPlugConstants.h"
  "IPlug/IPlugDelegate_select.h"
  "IPlug/IPlugEditorDelegate.h"
  "IPlug/IPlugLogger.h"
  "IPlug/IPlugMidi.h"
  "IPlug/IPlugParameter.cpp"
  "IPlug/IPlugParameter.h"
  "IPlug/IPlugPaths.cpp"
  "IPlug/IPlugPaths.h"
  "IPlug/IPlugPlatform.h"
  "IPlug/IPlugPluginBase.cpp"
  "IPlug/IPlugPluginBase.h"
  "IPlug/IPlugProcessor.cpp"
  "IPlug/IPlugProcessor.h"
  "IPlug/IPlugQueue.h"
  "IPlug/IPlugStructs.h"
  "IPlug/IPlugSWELL.h"
  "IPlug/IPlugTimer.cpp"
  "IPlug/IPlugTimer.h"
  "IPlug/IPlugUtilities.h"
  "IPlug/ISender.h")

if (WIN32)
  set(IPLUG_SOURCE ${IPLUG_SOURCE}
    "IGraphics/Platforms/IGraphicsWin.cpp"
    "IGraphics/Platforms/IGraphicsWin.h")
endif ()

add_library(iplug ${IPLUG_SOURCE})
target_link_libraries(iplug PUBLIC wdl)
target_compile_definitions(iplug PUBLIC IGRAPHICS_GL3 IGRAPHICS_NANOVG NOMINMAX)
target_include_directories(iplug
  PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}/IPlug"
    "${CMAKE_CURRENT_SOURCE_DIR}/IPlug/Extras"
    "${CMAKE_CURRENT_SOURCE_DIR}/IPlug/VST3"
    "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics"
    "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/Controls"
    "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/Extras"
    "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/Platforms"
    "${CMAKE_CURRENT_SOURCE_DIR}/IGraphics/Drawing"
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/STB"
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/yoga"
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/yoga/yoga"
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/glad_GL3/include"
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/nanovg/src"
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/nanosvg/src"
  PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/IGraphics/glad_GL3/src"
)

if (WIN32)
  target_link_libraries(iplug PUBLIC shlwapi.lib comctl32.lib wininet.lib)
endif ()

set(IPLUG_VST3_SOURCE
  "IPlug/VST3/IPlugVST3.cpp"
  "IPlug/VST3/IPlugVST3.h"
  "IPlug/VST3/IPlugVST3_Common.h"
  "IPlug/VST3/IPlugVST3_Controller.cpp"
  "IPlug/VST3/IPlugVST3_Controller.h"
  "IPlug/VST3/IPlugVST3_ControllerBase.h"
  "IPlug/VST3/IPlugVST3_Defs.h"
  "IPlug/VST3/IPlugVST3_Parameter.h"
  "IPlug/VST3/IPlugVST3_Processor.cpp"
  "IPlug/VST3/IPlugVST3_Processor.h"
  "IPlug/VST3/IPlugVST3_ProcessorBase.cpp"
  "IPlug/VST3/IPlugVST3_ProcessorBase.h"
  "IPlug/VST3/IPlugVST3_View.h")

add_library(iplug-vst3 ${IPLUG_VST3_SOURCE})
target_compile_definitions(iplug-vst3 PUBLIC VST3_API)
target_link_libraries(iplug-vst3 PUBLIC iplug iplug-vst3core)

function (iplug_add_target)
  set(OPTION_ARGS
    BUILD_VST BUILD_AAX)
  set(ONE_VALUE_ARGS
    TARGET NAME TYPE VST3_SUBCATEGORY UNIQUE_ID
    MANUFACTURER MANUFACTURER_ID VERSION
    VERSION_HEX URL EMAIL COPYRIGHT
    HAS_UI HOST_RESIZE CHANNEL_IO)
  set(MULTI_VALUE_ARGS BUILD_FORMAT SOURCE DEFINE)
  cmake_parse_arguments(PLUGIN_CONFIG
    "${OPTION_ARGS}"
    "${ONE_VALUE_ARGS}"
    "${MULTI_VALUE_ARGS}"
    ${ARGN})

  ## ---- Argument Checks ----

  if (${PLUGIN_CONFIG_NAME} STREQUAL "")
    message("NAME is not defined!")
  endif ()

  if (${PLUGIN_CONFIG_MANUFACTURER} STREQUAL "")
    message("MANUFACTURER is not defined!")
  endif ()

  if (${PLUGIN_CONFIG_TYPE} STREQUAL "")
    message("TYPE is not specified!")
  else ()
    string(TOLOWER ${PLUGIN_CONFIG_TYPE} PLUGIN_CONFIG_TYPE_LOWER)
    if (${PLUGIN_CONFIG_TYPE_LOWER} STREQUAL "effect")
      set(PLUGIN_CONFIG_TYPE_ID 0)
    elseif (${PLUGIN_CONFIG_TYPE_LOWER} STREQUAL "instrument")
      set(PLUGIN_CONFIG_TYPE_ID 1)
    else (${PLUGIN_CONFIG_TYPE_LOWER} STREQUAL "midieffect")
      set(PLUGIN_CONFIG_TYPE_ID 2)
    endif ()
  endif ()

  if (${PLUGIN_CONFIG_UNIQUE_ID} STREQUAL "")
    message("UNIQUE_ID is not defined!")
  endif ()

  if (${PLUGIN_CONFIG_MANUFACTURER_ID} STREQUAL "")
    message("MANUFACTURER_ID is not defined!")
  endif ()

  if (${PLUGIN_CONFIG_CHANNEL_IO} STREQUAL "")
    message("CHANNEL_IO is not specified!")
  endif ()

  ## ---- VST3 plugin target setup ----

  set(VST3_PLUGIN_TARGET "${PLUGIN_CONFIG_TARGET}-vst3")
  add_library(${VST3_PLUGIN_TARGET} SHARED
    ${PLUGIN_CONFIG_SOURCE})
  target_link_libraries(${VST3_PLUGIN_TARGET} PRIVATE iplug-vst3)
  set_target_properties(${VST3_PLUGIN_TARGET} PROPERTIES SUFFIX ".vst3")
  set_target_properties(${VST3_PLUGIN_TARGET} PROPERTIES DEBUG_POSTFIX "-debug")

  target_compile_definitions(
    ${VST3_PLUGIN_TARGET}
    PUBLIC
      PLUG_CMAKE_MODE=1
      PLUG_NAME="${PLUGIN_CONFIG_NAME}"
      PLUG_TYPE=${PLUGIN_CONFIG_TYPE_ID}
      PLUG_VERSION_HEX=${PLUGIN_CONFIG_VERSION_HEX}
      PLUG_VERSION_STR="${PLUGIN_CONFIG_VERSION}"
      PLUG_UNIQUE_ID=${PLUGIN_CONFIG_UNIQUE_ID}
      PLUG_MFR="${PLUGIN_CONFIG_MANUFACTURER}"
      PLUG_MFR_ID=${PLUGIN_CONFIG_MANUFACTURER_ID}
      PLUG_CHANNEL_IO="${PLUGIN_CONFIG_CHANNEL_IO}"
      PLUG_COPYRIGHT_STR="${PLUGIN_CONFIG_COPYRIGHT}"
      VST3_SUBCATEGORY="${PLUGIN_CONFIG_VST3_SUBCATEGORY}"
      ${PLUGIN_CONFIG_DEFINE})

  if (NOT ${PLUGIN_CONFIG_URL} STREQUAL "")
    target_compile_definitions(
      ${VST3_PLUGIN_TARGET} PUBLIC PLUG_URL_STR="${PLUGIN_CONFIG_URL}")
  endif ()

  if (NOT ${PLUGIN_CONFIG_EMAIL} STREQUAL "")
    target_compile_definitions(
      ${VST3_PLUGIN_TARGET} PUBLIC PLUG_EMAIL_STR="${PLUGIN_CONFIG_EMAIL}")
  endif ()

  if (PLUGIN_CONFIG_HAS_UI)
    target_compile_definitions(${VST3_PLUGIN_TARGET} PUBLIC PLUG_HAS_UI=1)
  endif ()

  if (PLUGIN_CONFIG_HOST_RESIZE)
    target_compile_definitions(${VST3_PLUGIN_TARGET} PUBLIC PLUG_HOST_RESIZE=1)
  else ()
    target_compile_definitions(${VST3_PLUGIN_TARGET} PUBLIC PLUG_HOST_RESIZE=0)
  endif ()
endfunction ()

if (IPLUG_BUILD_EXAMPLES)
  add_subdirectory(Examples/CMake)
endif ()