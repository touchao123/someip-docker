## Intro

## Feature overview
*   [x] **Easy to read** like an article
*   [x] **Feature overview and Contents** for fast orientation
*   [ ] **Visuals** to keep users engaged

## Contents

## What is this?

This project is an exhaustive README template that you can customize to your needs.
You can either add sections you like or remove sections you don't like. But you have
every time an example in front of you, from which you can derive from.

## Why should I use this?

There are many README templates out there so why this one? The two main reasons for this are
that they contain often too little content or they are not easy to read or navigate through.

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

# Copy the content
```bash
    cd run-script/
    ./create-someip-testenv
```
# Here two containers come to you, one is named server the other is named client.
# Login the targets by any of the 'vcc' or 'vss', they are responding to the client and server.
#
```bash
    ./vcc
```
# or
```bash
    ./vss
```
# Destroy both containers by 'delete-someip-testenv'
```bash
    ./delete-someip-testenv
```
That's all,have fun!

