FROM chao123/someip-base

ARG USERNAME=someip
ARG PASSWORD=someip

RUN groupadd someip
RUN useradd -d /home/$USERNAME -ms /bin/bash -g someip -G sudo $USERNAME

RUN  mkdir -p /home/someip/vsomeip-build
RUN cd /home/someip/vsomeip-build && \
    git clone https://github.com/COVESA/vsomeip.git && \
    cd vsomeip && \
    git checkout 3.1.20.3 && \
    rm -rf build && mkdir -p build && cd build && \
    cmake -D ENABLE_SIGNAL_HANDLING=1 -D CMAKE_INSTALL_PREFIX=/usr .. && \
    make -j4 && make install && \
    cd ../..


