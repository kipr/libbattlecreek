################################################################################
#   libbattlecreek CMake Build File                                                 #
################################################################################

project(libbattlecreek)

cmake_minimum_required(VERSION 2.8)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake") 
find_package(Daylite REQUIRED)
find_package(BsonBind REQUIRED)

set(CMAKE_C_FLAGS ${C_FLAGS})
set(CMAKE_CXX_FLAGS ${CXX_FLAGS})

set(INCLUDE ${libbattlecreek_SOURCE_DIR}/include)


include_directories(include ${CMAKE_BINARY_DIR})
include_directories(${DAYLITE_INCLUDE_DIRS})

add_bson_binds(BSON_BIND_INCLUDES
  src/accel_state.bsonbind
  src/analog_states.bsonbind
  src/battery_state.bsonbind
  src/battlehill_state.bsonbind
  src/blob.bsonbind
  src/camera_config.bsonbind
  src/channel_config.bsonbind
  src/channel_data.bsonbind
  src/digital_states.bsonbind
  src/frame_data.bsonbind
  src/gyro_state.bsonbind
  src/imu_state.bsonbind
  src/magneto_state.bsonbind
  src/motor_state.bsonbind
  src/motor_states.bsonbind
  src/pid_state.bsonbind
  src/pid_states.bsonbind
  src/robot_states.bsonbind
  src/servo_states.bsonbind
  src/set_accel_state.bsonbind
  src/set_battlehill_state.bsonbind
  src/set_digital_state.bsonbind
  src/set_gyro_state.bsonbind
  src/set_imu_state.bsonbind
  src/set_magneto_state.bsonbind
  src/set_motor_state.bsonbind
  src/set_pid_state.bsonbind
  src/set_servo_state.bsonbind
  src/settings.bsonbind
)

SET(BSON_BIND_INCLUDES_TMP "")
FOREACH(f ${BSON_BIND_INCLUDES})
  LIST(APPEND BSON_BIND_INCLUDES_TMP "${CMAKE_CURRENT_BINARY_DIR}/${f}")
ENDFOREACH(f)
SET(BSON_BIND_INCLUDES ${BSON_BIND_INCLUDES_TMP})

file(GLOB INCLUDES ${BSON_BIND_INCLUDES})

add_custom_target(battlecreek ALL DEPENDS ${BSON_BIND_INCLUDES})

################################################################################
#   Install                                                                    #
################################################################################

install(FILES ${BSON_BIND_INCLUDES} DESTINATION include/battlecreek)

