FROM debian:unstable-slim

RUN apt update -y && apt install tar gcc gcc-multilib build-essential libgmp-dev libmpfr-dev libmpc-dev python3-dev git flex bison -y 

RUN cd /root && git clone https://github.com/gcc-mirror/gcc.git gcc && mkdir gcc-build && cd gcc-build && ../gcc/configure && make -j 8 && make install && cd /root && rm -rf gcc && rm -rf gcc-build
