FROM chao123/someip-core

ARG USERNAME=someip
ARG PASSWORD=someip

RUN apt-get -y install boxes
RUN apt-get -y install cowsay fortune

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

RUN mkdir -p /var/run/sshd

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN chown -R $USERNAME: /home/$USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd

EXPOSE 22
CMD  ["/usr/sbin/sshd", "-D"]
