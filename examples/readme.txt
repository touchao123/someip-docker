

cmake -B build examples
cmake --build build

VCM&tcp:
env VSOMEIP_CONFIGURATION=./examples/config/vsomeip_server.json VSOMEIP_APPLICATION_NAME=service-sample ./build/notify-sample


CCCM&tcp:
env VSOMEIP_CONFIGURATION=./examples/config/vsomeip_client.json VSOMEIP_APPLICATION_NAME=client-sample ./build/subscribe-sample
