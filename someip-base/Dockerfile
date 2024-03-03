#Download base image ubuntu 22.04 LTS
FROM ubuntu:22.04


# ENV TZ=Asia/Shanghai
# RUN mkdir /usr/share/zoneinfo/Asia \
#   && ln -snf /usr/share/zoneinfo/PRC /usr/share/zoneinfo/$TZ \
#   && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
#   && echo $TZ > /etc/timezone

RUN     apt-get update 
RUN     \
        apt-get install -y cmake \
		libboost-all-dev \
		vim \
		curl \
		net-tools \
		inetutils-ping \
		wget \
		gdb  \
		sudo \
		tcpdump


RUN apt-get install -y unzip && \
    apt-get install -y openssh-server 

RUN apt-get install -y  \
		       git  \
		       build-essential \
			   pkg-config \
		       locales 

RUN locale-gen en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8

ARG USERNAME=ubuntu
ARG PASSWORD=ubuntu

RUN groupadd ubuntu
RUN useradd -d /home/$USERNAME -ms /bin/bash -g ubuntu -G sudo $USERNAME

RUN echo "\n  \
export PS1='\[\e[31;7m\][\u@\h \w]\$ \[\e[m\]' \n " \
>> /home/$USERNAME/.bashrc

RUN chown -R $USERNAME: /home/$USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd
