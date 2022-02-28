[![slack](https://slack.binary.ninja/badge.svg)](https://slack.binary.ninja/)

# Binary Ninja API

This repository contains documentation and source code for the [Binary Ninja](https://binary.ninja/) reverse engineering platform API.

## Branches

Please note that the [dev](/Vector35/binaryninja-api/tree/dev/) branch tracks changes on the `dev` build of Binary Ninja and is generally the place where all pull requests should be submitted to. However, the [master](/Vector35/binaryninja-api/tree/master/) branch tracks the `stable` build of Binary Ninja which is the default version run after installation. There is online documentation for both the [stable branch](https://api.binary.ninja/) and [dev branch](https://dev-api.binary.ninja).

## Contributing

Public contributions are welcome to this repository. All the API and documentation in this repository is licensed under an MIT license, however, the API interfaces with a closed-source commercial application, [Binary Ninja](https://binary.ninja).

If you're interested in contributing when you submit your first PR, you'll receive a notice from [CLA Assistant](https://cla-assistant.io/) that allows you to sign our [Contribution License Agreement](https://binary.ninja/cla.pdf) online.

## Issues

The issue tracker for this repository tracks not only issues with the source code contained here but also the broader Binary Ninja product.

## Usage and Build Instructions

To write Binary Ninja plugins using C++, you'll need to build the C++ API found in the root of this repo. The C++ API is built into a static library, which plugins and programs can then link against. The compiled API contains names and functions you can use from your plugins, but most of the implementation is missing until you link against the `binaryninjacore` library.

Building the API library is done similarly to most CMake-based projects; the basic steps are outlined as follows:

```Bash
# Get the source
git clone https://github.com/Vector35/binaryninja-api.git
cd binaryninja-api
git submodule update --init --recursive

# Configure an out-of-source build setup
cmake -S . -B build # <additional arguments here>

# Compile
cmake --build build -j8
```

In addition to the default build setup you may want to:

- **Build examples.** To build the [API examples](#examples), pass `-DBN_API_BUILD_EXAMPLES=ON` to CMake when configuring the build. After the build succeeds, you can install the built plugins by running the `install` target. When using the "Unix Makefiles" build generator, this looks like: `make install`.
- **Build UI plugins.** You will need Qt 6.1.3 (as of writing) installed to build UI plugins.
- **Build headlessly.** If you are using a headless Binary Ninja distribution or you do not wish to build UI plugins, pass `-DHEADLESS=ON` to CMake when configuring the build.

### Troubleshooting

- If Binary Ninja is installed at a different location than the platform default (defined in CMakeLists.txt), you will likely get an error stating "Binary Ninja Core Not Found." Specify the path to your Binary Ninja installation with by passing `-DBN_INSTALL_DIR=/path/to/binaryninja/installation` to CMake when configuring the build setup.
- Since Binary Ninja is a 64-bit only product, ensure that you are using a 64-bit compiling and linking environment. Errors on windows like LNK1107 might indicate that your bits don't match.

## Examples

There are many examples available. The [Python examples folder ](https://github.com/Vector35/binaryninja-api/tree/dev/python/examples) demonstrates many different applications of the Python API, while native examples include:

* [bin-info](https://github.com/Vector35/binaryninja-api/tree/dev/examples/bin-info) is a standalone executable that prints some information about a given binary to stdout (only usable with licenses that support headless API access)
* [breakpoint](https://github.com/Vector35/binaryninja-api/tree/dev/examples/breakpoint) is a plugin that allows you to select a region within an x86 binary and use the context menu to fill it with breakpoint bytes
* [command-line disassm](https://github.com/Vector35/binaryninja-api/tree/dev/examples/cmdline_disasm) demonstrates how to dump disassembly to the command-line (only usable with licenses that support headless API access)
* [llil-parser](https://github.com/Vector35/binaryninja-api/tree/dev/examples/llil_parser) parses Low-Level IL, demonstrating how to match types and use a visitor class (only usable with licenses that support headless API access)
* [mlil-parser](https://github.com/Vector35/binaryninja-api/tree/dev/examples/mlil_parser) parses Medium-Level IL, demonstrating how to match types and use a visitor class (only usable with licenses that support headless API access)
* [print_syscalls](https://github.com/Vector35/binaryninja-api/tree/dev/examples/print_syscalls) is a standalone executable that prints the syscalls used in a given binary (only usable with licenses that support headless API access)
* [triage](https://github.com/Vector35/binaryninja-api/tree/dev/examples/triage) is a fully featured plugin that is shipped and enabled by default, demonstrating how to do a wide variety of tasks including extending the UI through QT
* [workflows](https://github.com/Vector35/binaryninja-api/tree/dev/examples/workflows) is a collection of plugins that demonstrate using Workflows to extend the analysis pipeline
* [x86 extension](https://github.com/Vector35/binaryninja-api/tree/dev/examples/x86_extension) creates an architecture extension which shows how to modify the behavior of the build-in architectures without creating a complete replacement

## Licensing

Some components may be released under compatible but slightly different open source licenses and will have their own LICENSE file as appropriate.
