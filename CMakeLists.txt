cmake_minimum_required (VERSION 2.8.11)

project (aws_iot)


if(APPLE)
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -std=c11")
set(CMAKE_CXX_FLAGS_DEBUG   "-O0 -g -std=c11")
else(APPLE)
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -std=c11")
set(CMAKE_CXX_FLAGS_DEBUG   "-O0 -ggdb -g3 -std=c11")
set(CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++")
endif(APPLE)


add_library(awsiot external_libs/jsmn/jsmn.c  platform/linux/mbedtls/network_mbedtls_wrapper.c  ${CMAKE_SOURCE_DIR}/src/aws_iot_json_utils.c src/aws_iot_mqtt_client.c src/aws_iot_mqtt_client_common_internal.c src/aws_iot_mqtt_client_connect.c src/aws_iot_mqtt_client_publish.c src/aws_iot_mqtt_client_subscribe.c src/aws_iot_mqtt_client_unsubscribe.c src/aws_iot_mqtt_client_yield.c src/aws_iot_shadow.c src/aws_iot_shadow_actions.c src/aws_iot_shadow_json.c src/aws_iot_shadow_records.c platform/linux/common/timer.c)

target_include_directories(awsiot PUBLIC ${CMAKE_SOURCE_DIR}/config  ${CMAKE_SOURCE_DIR}/include ${CMAKE_SOURCE_DIR}/external_libs/jsmn ${CMAKE_SOURCE_DIR}/platform/linux/common ${CMAKE_SOURCE_DIR}/platform/linux/mbedtls ${MBEDTLS_INCLUDE} )

install(TARGETS awsiot DESTINATION lib)
install(FILES include/aws_iot_error.h include/timer_interface.h platform/linux/common/timer_platform.h platform/linux/mbedtls/network_platform.h  DESTINATION include)
install(FILES include/aws_iot_log.h include/network_interface.h DESTINATION include)
install(FILES include/aws_iot_mqtt_client.h include/aws_iot_version.h include/aws_iot_mqtt_client_interface.h DESTINATION include)
install(FILES include/aws_iot_log.h DESTINATION include)
install(FILES include/aws_iot_shadow_interface.h include/aws_iot_shadow_json_data.h   DESTINATION include)


