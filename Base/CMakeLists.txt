cmake_minimum_required(VERSION 2.8.12)

set (CMAKE_CXX_STANDARD 17)

add_library(Base STATIC
   "DeviceDescriptionLoader.cpp"
   "Midi1OutputManager.cpp"
   "MidiDumper.cpp"
   "MidiInMsgHandler.cpp"
   "MidiOutMsgHandler.cpp"
   "MidiRouter.cpp"
   "MusicDevice.cpp"
   "MusicDeviceHolder.cpp"
   "ParameterMapper.cpp"
   "SoundPresets.cpp"
   "TapTempoHandler.cpp"
   "TempoHandler.cpp"
   "TransportControl.cpp"
   "ValueCurve.cpp"
)

target_include_directories(Base
   PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_libraries(Base
   PUBLIC  Util
   PUBLIC  midi
   PRIVATE usbmidi
   PRIVATE Loguru
)

option(__INSERT_DUMMY_MIDI_DEVICES__ "insert dummy devices for testing" OFF)
if(${__INSERT_DUMMY_MIDI_DEVICES__})
   target_compile_definitions(Base PUBLIC "__INSERT_DUMMY_MIDI_DEVICES__")
   target_link_libraries(Base PRIVATE MidiMediumDummy)
endif(${__INSERT_DUMMY_MIDI_DEVICES__})
