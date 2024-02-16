#Download base image ubuntu 22.04 LTS
FROM ubuntu:22.04

# COPY sources.list /etc/apt/sources.list
# COPY zoneinfo/PRC /usr/share/zoneinfo/PRC
# ENV TZ=Asia/Shanghai
# RUN mkdir /usr/share/zoneinfo/Asia \
#   && ln -snf /usr/share/zoneinfo/PRC /usr/share/zoneinfo/$TZ \
#   && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
#   && echo $TZ > /etc/timezone

#RUN dpkg --add-architecture i386 && \
RUN     apt-get update 
RUN     \
        apt-get install -y cmake \
		libboost-all-dev \
#		asciidoc \
#		doxygen \
	 	# libsystemd-dev \
		# vim \
		# iproute2 \
	 	# traceroute \
		curl \
		dnsutils \
		net-tools \
		inetutils-ping \
		wget \
		gdb  \
		# netcat-openbsd \
		sudo \
		tcpdump
		# apt-utils 
		

# RUN DEBIAN_FRONTEND=noninteractive apt-get install wireshark -y &&  \
#     apt-get install -y tshark

RUN apt-get install -y unzip && \
    apt-get install -y unrar  && \
    apt-get install -y openssh-server 

RUN apt-get install -y  \
		       git  \
		       diffstat  \
		       texinfo  \
#		       gcc-multilib \
		       build-essential \
		    #    chrpath \
		       socat \
		    #    libsdl1.2-dev \
		       cpio \
		       locales 


RUN echo "\n  \
export PS1='\[\e[31;7m\][\u@\h \w]\$ \[\e[m\]' \n " \
>> ~/.bashrc

RUN locale-gen en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8

ARG USERNAME=someip
ARG PASSWORD=someip

RUN groupadd someip
RUN useradd -d /home/$USERNAME -ms /bin/bash -g someip -G sudo $USERNAME


RUN chown -R $USERNAME: /home/$USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd
