FROM chao123/someip-base:latest

ARG USERNAME=someip
ARG PASSWORD=someip

RUN apt-get -y install \
    boxes \
    cowsay fortune


RUN mkdir -p /home/someip/protocolbuf
RUN cd /home/someip/protocolbuf && \
    git clone https://github.com/protocolbuffers/protobuf.git && \
    cd protobuf && \
    git submodule update --init --recursive && \
    cmake -B build -DCMAKE_CXX_STANDARD=14 &&\
    cmake --build build --parallel $(nproc) && \
    make install -C build && \
    rm build -rf && \
    cd ../..

RUN mkdir -p /home/someip/vsomeip-build
RUN cd /home/someip/vsomeip-build && \
    git clone https://github.com/COVESA/vsomeip.git && \
    cd vsomeip && \
    git checkout 3.1.20.3 && \
    rm -rf build && mkdir -p build && cd build && \
    cmake -B build -D ENABLE_SIGNAL_HANDLING=1 -D CMAKE_INSTALL_PREFIX=/usr .. && \
    cmake --build build --parallel $(nproc) && \
    make install -C build && \
    rm -rf build && \
    cd ../..


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

RUN groupadd $USERNAME
RUN useradd -d /home/$USERNAME -ms /bin/bash -g someip -G sudo $USERNAME

RUN echo "$USERNAME:$PASSWORD" | chpasswd

RUN mkdir -p /var/run/sshd

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


EXPOSE 22
CMD  ["/usr/sbin/sshd", "-D"]
