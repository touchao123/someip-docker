FROM chao123/someip-base

ARG USERNAME=someip
ARG PASSWORD=someip

RUN groupadd someip
RUN useradd -d /home/$USERNAME -ms /bin/bash -g someip -G sudo $USERNAME

RUN echo "$USERNAME:$PASSWORD" | chpasswd

RUN mkdir -p /home/someip/vsomeip-build
RUN cd /home/someip/vsomeip-build && \
    git clone https://github.com/COVESA/vsomeip.git && \
    cd vsomeip && \
    git checkout 3.1.20.3 && \
    rm -rf build && mkdir -p build && cd build && \
    cmake -B build -D ENABLE_SIGNAL_HANDLING=1 -D CMAKE_INSTALL_PREFIX=/usr .. && \
    cmake --build build --parallel 4 && \
    make install -C build && \
    rm -rf build && \
    cd ../..


