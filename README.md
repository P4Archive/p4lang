# P4 ➡ LLVM
P4lang is an LLVM front-end for P4, a networking language.

This project is built upon open-source P4 compiler called [p4c](https://github.com/p4lang/p4c).
The LLVM IR emitter is a pass over p4c IR. We reuse the p4c front-end and translate p4c IR to LLVM IR.

![Image](images/blockdiagram.png)
## Getting started
Install LLVM from source. We are using LLVM 7.0, not tested on the other versions.

* `git clone https://llvm.org/git/llvm.git`
* `cd llvm && mkdir build && cd build`
* `cmake ../`
* `make `

Either do `make install` after `make` or export the path of llvm binaries.

Clone the P4lang repository. It includes submodules, so be sure to use --recursive to pull them in:

`git clone --recursive https://github.com/IITH-Compilers/p4lang.git`

If you forget to use `--recursive`, you can update the submodules at any time using:

`git submodule update --init --recursive`

### Install dependencies.

Dependencies for this repository are same as the p4c compiler. We are listing them here for ease.

* A C++11 compiler. GCC 4.9 or later or Clang 3.3 or later is required.
* git for version control
* GNU autotools for the build process
* CMake 3.0.2 or higher
* Boehm-Weiser garbage-collector C++ library
* GNU Bison and Flex for the parser and lexical analyzer generators.
* Google Protocol Buffers 3.0 or higher for control plane API generation
* GNU multiple precision library GMP
* C++ boost library (minimally used)
* Python 2.7 for scripting and running tests


#### On Ubuntu you can use:

`sudo apt-get install g++ git automake libtool libgc-dev bison flex libfl-dev libgmp-dev libboost-dev libboost-iostreams-dev libboost-graph-dev pkg-config python python-scapy python-ipaddr tcpdump cmake`

##### Install protobuf 3.2.0

* `git clone https://github.com/google/protobuf.git`
* `git checkout v3.2.0`
* `./autogen.sh`
* `./configure`
* `make`
* `make check`
* `sudo make install`
* `sudo ldconfig # refresh shared library cache.`

##### Build p4lang in a subdirectory named build.

* `mkdir build && cd build`
* `cmake ..`
* `make -j4`
* `make -j4 check`




## Following are the supported constructs of P4 (as of now)

`Bool,
Bits,
Structures,
Header,
Header union,
Typedef,
Select statements,
States,
Transition,
If Statements,
Assignment statements,
Constants,
Arithmetic operations,
Complementation,
Negation,
Boolean operations,
Logical operations,
Relational operations,
Ternary operator,
Parser block and
Control block`
## How to run?
Once make is successful, execute `p4c` in build directory to run the code. For example,

`./p4c --target ebpf-v1model-p4org ../p4lang/testdata/p4_16_samples/toy_ebpf.p4`

This would create `toy_ebpf.p4i.ll`, a file with LLVM IR equivalent of `toy_ebpf.p4`. `toy_ebpf.p4i.ll` file would be found under P4’s build directory.
