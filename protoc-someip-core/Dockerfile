FROM chao123/someip-core


RUN mkdir -p /home/someip/protocolbuf
RUN cd /home/someip/protocolbuf && \
    git clone https://github.com/protocolbuffers/protobuf.git && \
    cd protobuf && \
    git submodule update --init --recursive && \
    cmake -B build -DCMAKE_CXX_STANDARD=14 &&\
    cmake --build build --parallel 4 && \
    make install -C build && \
    rm build -rf && \
    cd ../..
