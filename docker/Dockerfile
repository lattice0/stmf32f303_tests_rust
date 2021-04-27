FROM ubuntu:focal

WORKDIR /home/project

RUN export DEBIAN_FRONTEND=noninteractive && apt-get update\
    && apt-get install -y build-essential curl autoconf git m4 \
    iproute2 clang libpq-dev clang gdb-multiarch libusb-1.0-0-dev pkg-config

ENV PATH="/root/.cargo/bin:/usr/local/cmake/bin:${PATH}"

RUN curl --proto '=https' --tlsv1.2 -o rust.sh https://sh.rustup.rs\
    && /bin/bash rust.sh -y

RUN rustup component add rust-analysis --toolchain stable-x86_64-unknown-linux-gnu \
    && rustup component add rust-src --toolchain stable-x86_64-unknown-linux-gnu \
    && rustup component add rls --toolchain stable-x86_64-unknown-linux-gnu \
    && rustup target install thumbv7m-none-eabi

COPY openocd-0.11.0.tar.bz2 /home/project/openocd.tar.bz2

RUN tar -xvjf /home/project/openocd.tar.bz2

RUN cd /home/project/openocd-0.11.0 && ./configure && make && make install