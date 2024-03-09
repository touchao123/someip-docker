FROM chao123/someip-base:latest

ARG USERNAME=someip
ARG PASSWORD=someip

RUN groupadd $USERNAME
RUN useradd -d /home/$USERNAME -ms /bin/bash -g someip -G sudo $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd


RUN apt-get -y install \
    boxes \
    cowsay \
    fortune \
    openssh-server 

RUN echo "\n  \
export PS1='\[\e[32;7m\][\u@\h \w]\$ \[\e[m\]' \n\
clear \n\
echo ' SOME/IP Development Environment ' | boxes -d columns -ac -s 46x6 \n\
echo '~~~ Have fun!' \n\
/usr/games/fortune | /usr/games/cowsay -W 55 -e @@ -T ~~\n\
echo -e \n\
echo -e \n\
cd ~ " \
>> /home/$USERNAME/.bashrc

ARG PB_BUILD=/home/someip/protocolbuf
RUN mkdir -p ${PB_BUILD}
RUN cd ${PB_BUILD} && \
    git clone https://github.com/protocolbuffers/protobuf.git && \
    cd protobuf && \
    git submodule update --init --recursive && \
    cmake -B build -DCMAKE_CXX_STANDARD=14 &&\
    cmake --build build --parallel $(nproc) && \
    make install -C build && \
    chown -R ${USERNAME}:${USERNAME} ${PB_BUILD}  && \
    rm build -rf && \
    cd ../..

ARG SIP_BUILD=/home/someip/vsomeip-build
RUN mkdir -p ${SIP_BUILD}
RUN cd ${SIP_BUILD} && \
    git clone https://github.com/COVESA/vsomeip.git && \
    cd vsomeip && \
    git checkout 3.1.20.3 && \
    cmake -B build -D ENABLE_SIGNAL_HANDLING=1 -D CMAKE_INSTALL_PREFIX=/usr && \
    cmake --build build --parallel $(nproc) && \
    make install -C build && \
    chown -R ${USERNAME}:${USERNAME} ${SIP_BUILD}  && \
    rm -rf build && \
    cd ../..



# Compiling Mosquitto
ENV VERSION=1.6.15 \
    DOWNLOAD_SHA256=5ff2271512f745bf1a451072cd3768a5daed71e90c5179fae12b049d6c02aa0f \
    GPG_KEYS=A0D6EEA1DCAE49A635A3B2F0779B22DFB3E717B7 \
    LWS_VERSION=4.2.1 \
    LWS_SHA256=842da21f73ccba2be59e680de10a8cce7928313048750eb6ad73b6fa50763c51

ARG LWS_BUILD=/home/jlr/lws-build
ARG MOSQ_BUILD=/home/jlr/mosquitto-build
RUN apt-get -y install libssl-dev && \
    mkdir -p $LWS_BUILD && \
    wget https://github.com/warmcat/libwebsockets/archive/v${LWS_VERSION}.tar.gz -O /tmp/lws.tar.gz && \
    echo "$LWS_SHA256  /tmp/lws.tar.gz" | sha256sum -c - && \
    tar --strip=1 -xf /tmp/lws.tar.gz -C $LWS_BUILD && \
    rm /tmp/lws.tar.gz && \
    cd $LWS_BUILD && \
    cmake . \
        -DCMAKE_BUILD_TYPE=MinSizeRel \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DDISABLE_WERROR=ON \
        -DLWS_IPV6=ON \
        -DLWS_WITHOUT_BUILTIN_GETIFADDRS=ON \
        -DLWS_WITHOUT_CLIENT=ON \
        -DLWS_WITHOUT_EXTENSIONS=ON \
        -DLWS_WITHOUT_TESTAPPS=ON \
        -DLWS_WITH_EXTERNAL_POLL=ON \
        -DLWS_WITH_HTTP2=OFF \
        -DLWS_WITH_SHARED=OFF \
        -DLWS_WITH_ZIP_FOPS=OFF \
        -DLWS_WITH_ZLIB=OFF && \
    make -j "$(nproc)" && \
    rm -rf $LWS_BUILD/.cmake && \
    wget https://mosquitto.org/files/source/mosquitto-${VERSION}.tar.gz -O /tmp/mosq.tar.gz && \
    echo "$DOWNLOAD_SHA256  /tmp/mosq.tar.gz" | sha256sum -c - && \
    mkdir -p $MOSQ_BUILD && \
    tar --strip=1 -xf /tmp/mosq.tar.gz -C $MOSQ_BUILD && \
    rm /tmp/mosq.tar.gz && \
    make -C $MOSQ_BUILD -j "$(nproc)" \
        CFLAGS="-Wall -O2 -I$LWS_BUILD/include" \
        LDFLAGS="-L$LWS_BUILD/lib" \
        WITH_ADNS=no \
        WITH_DOCS=no \
        WITH_SHARED_LIBRARIES=yes \
        WITH_SRV=no \
        WITH_STRIP=yes \
        WITH_WEBSOCKETS=yes \
        prefix=/usr \
        binary && \
    groupadd mosquitto -g 1883 && \
    useradd -u 1883 -r -d /home/mosquitto -ms /bin/bash -g mosquitto -G sudo mosquitto && \
    mkdir -p /mosquitto/config /mosquitto/data /mosquitto/log && \
    install -d /usr/sbin/ && \
    install -s -m755 $MOSQ_BUILD/client/mosquitto_pub /usr/bin/mosquitto_pub && \
    install -s -m755 $MOSQ_BUILD/client/mosquitto_rr /usr/bin/mosquitto_rr && \
    install -s -m755 $MOSQ_BUILD/client/mosquitto_sub /usr/bin/mosquitto_sub && \
    install -s -m644 $MOSQ_BUILD/lib/libmosquitto.so.1 /usr/lib/libmosquitto.so.1 && \
    install -s -m755 $MOSQ_BUILD/src/mosquitto /usr/sbin/mosquitto && \
    install -s -m755 $MOSQ_BUILD/src/mosquitto_passwd /usr/bin/mosquitto_passwd && \
    install -m644 $MOSQ_BUILD/mosquitto.conf /mosquitto/config/mosquitto.conf && \
    install -Dm644 $LWS_BUILD/LICENSE /usr/share/licenses/libwebsockets/LICENSE && \
    install -Dm644 $MOSQ_BUILD/epl-v10 /usr/share/licenses/mosquitto/epl-v10 && \
    install -Dm644 $MOSQ_BUILD/edl-v10 /usr/share/licenses/mosquitto/edl-v10 && \
    chown -R mosquitto:mosquitto /mosquitto && \
    rm -rf /build


RUN mkdir -p /var/run/sshd

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


EXPOSE 22
CMD  ["/usr/sbin/sshd", "-D"]
