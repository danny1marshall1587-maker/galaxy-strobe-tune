cmake_minimum_required(VERSION 3.15)

project(GALAXY_STROBE_TUNE VERSION 1.0.0 LANGUAGES C CXX)

include(FetchContent)
FetchContent_Declare(
    juce
    GIT_REPOSITORY https://github.com/juce-framework/JUCE.git
    GIT_TAG origin/master
)
FetchContent_MakeAvailable(juce)

juce_add_plugin(GalaxyStrobeTune
    PRODUCT_NAME "Galaxy Strobe Tune"
    COMPANY_NAME "Galaxy"
    BUNDLE_ID com.galaxy.strobetune
    PLUGIN_MANUFACTURER_CODE Galx
    PLUGIN_CODE Strb
    FORMATS VST3 AU Standalone
    COPY_PLUGIN_AFTER_BUILD TRUE
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MIDI_EFFECT FALSE
    EDITOR_WANTS_KEYBOARD_FOCUS TRUE
)

target_sources(GalaxyStrobeTune
    PRIVATE
        Source/PluginProcessor.cpp
        Source/PluginProcessor.h
        Source/PluginEditor.cpp
        Source/PluginEditor.h
)

target_compile_definitions(GalaxyStrobeTune
    PUBLIC
        JUCE_WEB_BROWSER=0
        JUCE_USE_CURL=0
        JUCE_VST3_CAN_REPLACE_VST2=0
)

target_link_libraries(GalaxyStrobeTune
    PRIVATE
        juce::juce_audio_utils
        juce::juce_audio_processors
        juce::juce_gui_extra
        juce::juce_opengl
        juce::juce_dsp
)

juce_generate_juce_header(GalaxyStrobeTune)
