set(IPLUGEFFECT_SOURCE
  "IPlugEffect.cpp"
  "IPlugEffect.h")

iplug_add_target(
  # iPlug standard configurations
  TARGET            IPlugEffect
  NAME              IPlugEffect
  TYPE              Effect
  VST3_SUBCATEGORY  Fx
  VERSION           1.0.0
  VERSION_HEX       0x00010000
  UNIQUE_ID         0x9B73192C
  MANUFACTURER      AcmeInc
  MANUFACTURER_ID   0xFF798BC7
  EMAIL             spam@me.com
  COPYRIGHT         "Copyright 2020 Acme Inc"
  HAS_UI            TRUE
  HOST_RESIZE       TRUE
  CHANNEL_IO        "1-1 2-2"

  # Specifies which plugin format to build
  BUILD_FORMAT      VST3 VST2 AU

  # Define sources and compile definitions
  SOURCE            ${IPLUGEFFECT_SOURCE}
  DEFINE            IPLUG_EXAMPLE_RESOURCE_PATH="${IPLUG_EXAMPLE_RESOURCE_PATH}"
)

