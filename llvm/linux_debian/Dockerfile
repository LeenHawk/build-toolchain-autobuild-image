FROM debian:unstable-slim

RUN apt update -y && apt install tar clang lld libc++-dev libc++abi-dev libclang-rt-dev \
    cmake ninja-build build-essential git python3-dev libtbb-dev libxml2-dev libedit-dev \
    terminfo liblzma-dev swig lua5.3 liblua5.3-dev ocaml ocaml-findlib libctypes-ocaml-dev \
    doxygen graphviz ccache -y 

COPY /root/llvm.tar.gz /root/

RUN cd /root/ && tar -zxvf llvm.tar.gz build/ && cd build && cmake --build . --target install \
    && cd /root && rm -rf build \ 
    && echo "export LD_LIBRARY_PATH=/usr/local/lib/x86_64-unknown-linux-gnu/:$LD_LIBRARY_PATH" >> /etc/bash.bashrc 
