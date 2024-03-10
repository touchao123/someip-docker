# Copyright (C) 2015-2017 Bayerische Motoren Werke Aktiengesellschaft (BMW AG)
# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.

cmake_minimum_required (VERSION 2.8)

project (example)

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 14)
# target_compile_features(example PRIVATE cxx_std_14)

set (VSOMEIP_NAME vsomeip3)
set (PB_LIBRARY 
    spd_proto
    ${PROTOBUF_LIBRARY}
    )

# set(EXAMPLE_CONFIG_FILES
#     "./config/vsomeip.json"
# )

# Work around since Cmake linking absl issue 
find_package(PkgConfig)
pkg_search_module(TMP_PB REQUIRED protobuf)
set (PB_LIBRARY 
    ${PB_LIBRARY}
    ${TMP_PB_LIBRARIES}
    )

find_package(Protobuf REQUIRED)

add_subdirectory(schema)


# Examples
add_executable(request-sample request-sample.cpp )

target_include_directories(request-sample  PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(request-sample ${VSOMEIP_NAME} ${Boost_LIBRARIES} ${PB_LIBRARY})

add_executable(response-sample response-sample.cpp )
target_include_directories(response-sample  PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(response-sample ${VSOMEIP_NAME} ${Boost_LIBRARIES} ${PB_LIBRARY})

add_executable(subscribe-sample subscribe-sample.cpp )
target_include_directories(subscribe-sample  PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(subscribe-sample ${VSOMEIP_NAME} ${Boost_LIBRARIES} ${PB_LIBRARY})

add_executable(notify-sample notify-sample.cpp )
target_include_directories(notify-sample  PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(notify-sample ${VSOMEIP_NAME} ${Boost_LIBRARIES} ${PB_LIBRARY})

#add_dependencies(examples request-sample response-sample subscribe-sample notify-sample)

install (
    TARGETS request-sample response-sample subscribe-sample notify-sample
    RUNTIME DESTINATION "${INSTALL_BIN_DIR}" COMPONENT bin
)

###################################################################################################
