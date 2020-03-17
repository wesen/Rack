cmake_minimum_required(VERSION 3.10)

project(Rack)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_CXX_STANDARD_REQUIRED YES)
set(CMAKE_CXX_EXTENSIONS NO)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_compile_options(
    -Wall -Wextra -Wno-unused-parameter -g -O3 -march=nocona -funsafe-math-optimizations
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Darwin>:-mmacosx-version-min=10.7>
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Darwin>:-stdlib=libc++>
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Linux>:-Wsuggest-override>
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Windows>:-Wsuggest-override>
)

add_compile_definitions(
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Darwin>:ARCH_MAC>
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Linux>:ARCH_LIN>
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Windows>:ARCH_WIN>
    $<$<STREQUAL:${CMAKE_HOST_SYSTEM_NAME},Windows>:_USE_MATH_DEFINES>
)

add_subdirectory(plugins)

add_library(racklib SHARED)

target_include_directories(racklib
    PUBLIC
    include
    dep/include
    )
target_sources(racklib PRIVATE

    src/random.cpp
    src/ui.cpp
    src/svg.cpp
    src/keyboard.cpp
    src/core/CV_MIDI.cpp
    src/core/AudioInterface.cpp
    src/core/CV_CC.cpp
    src/core/CV_Gate.cpp
    src/core/plugin.cpp
    src/core/MIDI_Gate.cpp
    src/core/MIDI_CV.cpp
    src/core/Notes.cpp
    src/core/MIDI_Map.cpp
    src/core/Blank.cpp
    src/core/MIDI_CC.cpp
    src/audio.cpp
    src/dep.cpp
    src/midi.cpp
    src/bridge.cpp
    src/tag.cpp
    src/app/LedDisplay.cpp
    src/app/Knob.cpp
    src/app/ModuleWidget.cpp
    src/app/Scene.cpp
    src/app/ModuleBrowser.cpp
    src/app/MenuBar.cpp
    src/app/SvgSwitch.cpp
    src/app/SvgPort.cpp
    src/app/SvgButton.cpp
    src/app/LightWidget.cpp
    src/app/RackScrollWidget.cpp
    src/app/PortWidget.cpp
    src/app/common.cpp
    src/app/ParamWidget.cpp
    src/app/SvgKnob.cpp
    src/app/RackRail.cpp
    src/app/MultiLightWidget.cpp
    src/app/AudioWidget.cpp
    src/app/MidiWidget.cpp
    src/app/SvgPanel.cpp
    src/app/RackWidget.cpp
    src/app/SvgSlider.cpp
    src/app/CircularShadow.cpp
    src/app/Switch.cpp
    src/app/ModuleLightWidget.cpp
    src/app/CableWidget.cpp
    src/app/SvgScrew.cpp
    src/asset.cpp
    src/system.cpp
    src/patch.cpp
    src/event.cpp
    src/color.cpp
    src/app.cpp
    src/Quantity.cpp
    src/main.cpp
    src/settings.cpp
    src/gamepad.cpp
    src/string.cpp
    src/network.cpp
    src/plugin.cpp
    src/plugin/Model.cpp
    src/plugin/Plugin.cpp
    src/logger.cpp
    src/history.cpp
    src/rtmidi.cpp
    src/widget/SvgWidget.cpp
    src/widget/FramebufferWidget.cpp
    src/widget/ZoomWidget.cpp
    src/widget/Widget.cpp
    src/widget/OpenGlWidget.cpp
    src/ui/ChoiceButton.cpp
    src/ui/Tooltip.cpp
    src/ui/PasswordField.cpp
    src/ui/Slider.cpp
    src/ui/Button.cpp
    src/ui/MarginLayout.cpp
    src/ui/MenuOverlay.cpp
    src/ui/ScrollWidget.cpp
    src/ui/Menu.cpp
    src/ui/SequentialLayout.cpp
    src/ui/MenuEntry.cpp
    src/ui/RadioButton.cpp
    src/ui/MenuItem.cpp
    src/ui/TextField.cpp
    src/ui/Label.cpp
    src/ui/ProgressBar.cpp
    src/ui/List.cpp
    src/ui/MenuLabel.cpp
    src/ui/IconButton.cpp
    src/ui/MenuSeparator.cpp
    src/ui/ScrollBar.cpp
    src/dsp/minblep.cpp
    src/engine/Engine.cpp
    src/engine/Module.cpp
    src/engine/Port.cpp
    src/engine/ParamQuantity.cpp
    src/updater.cpp
    src/window.cpp
    )

