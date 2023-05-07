FROM debian:unstable-slim

RUN apt update -y && apt install tar gcc cmake \
          ninja-build build-essential git python3-dev libtbb-dev \
          libxml2-dev libedit-dev terminfo liblzma-dev swig lua5.3 liblua5.3-dev ocaml ocaml-findlib \
          libctypes-ocaml-dev doxygen ccache -y \
    && cd /root/ && git clone https://github.com/llvm/llvm-project.git && cd llvm-project && mkdir build && cd build \
    &&  cmake -G "Ninja" \
          -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;lld;lldb;libc;pstl;mlir;flang"   \
          -DLLVM_TARGETS_TO_BUILD=Native   -DCMAKE_BUILD_TYPE=Release   -DCLANG_DEFAULT_CXX_STDLIB=libc++   \
          -DCLANG_DEFAULT_RTLIB=compiler-rt   -DLLVM_ENABLE_RUNTIMES="compiler-rt;libcxx;libcxxabi;libunwind" \
          -DLIBCXX_USE_COMPILER_RT=YES   -DLIBCXXABI_USE_COMPILER_RT=YES   -DLIBCXXABI_USE_LLVM_UNWINDER=YES \
          -DLIBUNWIND_USE_COMPILER_RT=Yes   -DLIBCXX_ENABLE_PARALLEL_ALGORITHMS=YES    -DPSTL_PARALLEL_BACKEND="tbb" \
          -DCMAKE_BUILD_TYPE=Release -DLLVM_CCACHE_BUILD=ON ../llvm \
    &&  cmake --build . \
    &&  cmake --build . --target ocaml_doc \
    &&  cmake --build . --target install \
    &&  cd /root && rm -rf llvm-project 
