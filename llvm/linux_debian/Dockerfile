FROM debian:unstable-slim

RUN apt update -y && apt install tar clang lld cmake \
          ninja-build build-essential git python3-dev libtbb-dev \
          libxml2-dev libedit-dev terminfo liblzma-dev swig doxygen ccache -y 

RUN cd /root/ && git clone https://github.com/llvm/llvm-project.git && cd llvm-project && mkdir build && cd build \
    &&  cmake -G "Ninja" \
          -DCMAKE_C_COMPILER=clang \
          -DCMAKE_CXX_COMPILER=clang++ \
          -DLLVM_USE_LINKER=lld \
          -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;lld;lldb;libc;pstl;mlir"   \
          -DLLVM_TARGETS_TO_BUILD=Native   -DCMAKE_BUILD_TYPE=Release   -DCLANG_DEFAULT_CXX_STDLIB=libc++   \
          -DCLANG_DEFAULT_RTLIB=compiler-rt   -DLLVM_ENABLE_RUNTIMES="compiler-rt;libcxx;libcxxabi;libunwind" \
          -DLIBCXX_USE_COMPILER_RT=YES   -DLIBCXXABI_USE_COMPILER_RT=YES   -DLIBCXXABI_USE_LLVM_UNWINDER=YES \
          -DLIBUNWIND_USE_COMPILER_RT=Yes   -DLIBCXX_ENABLE_PARALLEL_ALGORITHMS=YES    -DPSTL_PARALLEL_BACKEND="tbb" \
          -DCMAKE_BUILD_TYPE=Release -DLLVM_CCACHE_BUILD=ON -DLLVM_ENABLE_LTO=Full ../llvm \
    &&  cmake --build . \
    &&  cmake --build . --target install \
    &&  cd /root && rm -rf llvm-project 
