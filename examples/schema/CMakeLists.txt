
# # Find required protobuf package
# find_package(protobuf CONFIG REQUIRED)


# set(example, fake_spd_acc)
# set(${example}_PROTOS fake_spd_acc.proto)

# # protobuf_generate(
# #     TARGET spd_proto
# #     LANGUAGE cpp 
# #     IMPORT_DIRS ${CMAKE_INCLUDE_SOURCE_DIR}
# #     PROTOC_OUT_DIR ${CMAKE_INCLUDE_SOURCE_DIR}
# #     fake_spd_acc.proto
# # )

# protobuf_generate(
#     TARGET spd_proto
#     IMPORT_DIRS ${CMAKE_INCLUDE_SOURCE_DIR}
#     PROTOC_OUT_DIR ${CMAKE_INCLUDE_SOURCE_DIR}
#     fake_spd_acc.proto
# )

# add_library(spd_proto #name
#     fake_spd_acc.pb.cc
# )


find_package(Protobuf REQUIRED)


set(PROTO_SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(PROTO_DST_DIR "${CMAKE_CURRENT_BINARY_DIR}")


file(GLOB PROTO_FILES "${PROTO_SRC_DIR}/*.proto")
protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS ${PROTO_FILES})


add_library(spd_proto ${PROTO_SRCS} ${PROTO_HDRS})
target_link_libraries(spd_proto ${PROTOBUF_LIBRARY})