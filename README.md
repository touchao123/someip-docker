## Intro

## Feature overview
*   [x] **Easy to use** 
*   [x] **Facility scripts** for fast login
*   [ ] **Visuals** to keep users engaged

## Contents

## What is this?

This project is a someip dockerized template that you can customize to your needs.
You can either use it for testing the protocal you like or develop the upon application. 

### Stacks layout

*   someip-stack        | => Interactive layer with user.
*   ... other stack     | => Others based the lower layer 'pb-sip'.
*   pb-sip              | => Add protocolBuffer basing on 'someip-core'.
*   someip-core         | => Resopnsible for compling the vsomeip stack.
*   someip-base         | => This is lowest layer for providing development tools of build-essential, 
                        |    cmake, git etc. which supporing the higher level's compiling.

## Getting Started

So how do you get this template to work for your project? It is easier than you think.

### Requirements

### Install

Use git to clone this repository into your computer.

```
git clone https://github.com/touchao123/someip-docker.git
```

### Usage

1> Trail the pre-built images as this:

```bash
    docker pull chao123/someip
    docker pull chao123/someip-base
    docker pull chao123/someip
```
2> Run them with the facility of scripts

### Bring up containers
```bash
    cd run-script/
    ./create-someip-testenv
```
Here two containers come to you, one is named server the other is named client.
### Login the targets 
By any of the 'vcc' or 'vss', they are responding to the client and server.

```bash
    ./vcc
```
or
```bash
    ./vss
```
### Destroy both containers 
by 'delete-someip-testenv'

```bash
    ./delete-someip-testenv
```
That's all,have fun!

