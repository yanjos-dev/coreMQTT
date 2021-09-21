cmake_minimum_required( VERSION 3.2.0 )

project(cmsis_build VERSION 1.0.1 DESCRIPTION "Project used for generating CMake targets for CMSIS packs.")

# Repository root directory path
set(ROOT_DIR "/home/ubuntu/repos/mqtt_fork/coreMQTT")

# MQTT library source files.
set( MQTT_SOURCES
     "${CMAKE_CURRENT_LIST_DIR}/../../source/core_mqtt.c"
     "${CMAKE_CURRENT_LIST_DIR}/../../source/core_mqtt_state.c" )

# MQTT Serializer library source files.
set( MQTT_SERIALIZER_SOURCES
     "${CMAKE_CURRENT_LIST_DIR}/../../source/core_mqtt_serializer.c" )

# MQTT library Public Include directories.
set( MQTT_INCLUDE_PUBLIC_DIRS
     "${CMAKE_CURRENT_LIST_DIR}/../../source/include"
     "${CMAKE_CURRENT_LIST_DIR}/../../source/interface" )

# Add the library CMake file containing metadata for source files and include paths
# include( ${ROOT_DIR}/mqttFilePaths.cmake )

#################### CMSIS target for the coreMQTT Client library ###################
add_library(core_mqtt_library)
target_sources(core_mqtt_library PUBLIC ${MQTT_SOURCES} ${MQTT_SERIALIZER_SOURCES})
target_include_directories(core_mqtt_library PUBLIC ${MQTT_INCLUDE_PUBLIC_DIRS})
set_target_properties(core_mqtt_library PROPERTIES DEFINE_SYMBOL "")
set_target_properties(core_mqtt_library PROPERTIES LINKER_LANGUAGE C)
