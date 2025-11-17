# CacheIQ: A Trace-Driven CPU Cache Simulator

## Overview
CacheIQ is a trace-driven CPU cache simulator written in modern C++. It allows computer science students and developers to study and analyze the behavior and performance impact of various cache designs and data access patterns.

## Specifications
This section details the fixed and flexible design constraints of the simulator.
* **Associativity**: Flexible (1 way - 1024 ways).
* **Cache line size**: 64 bytes.
* **Total cache size**: Flexible (8KB - 64KB).
* **Replacement policy**: Full LRU / Random Replacement.
* **Write policy**: Write-Through.
* **Allocation policy**: No-Write-Allocate.
* **Supported instructions**: Read / Write.
* **Instruction data size**: 4 bytes.
* **Data generation**: Random data.
* **Memory layout**: 32-bit addresses.
* **Address alignment**: 4 bytes.
* **RAM size**: 4096KB.
* **Output**: Standard output (CLI).
* **Output detail level**: Flexible (Minimal / Extended).

## Building the Project
### Prerequisites
To build and run this project, you need the following tools installed on your system:
1. **Operating System**: Windows, macOS, or Linux.
2. **C++ Compiler**: GCC, Clang, or MSVC (C++20 standard or newer).
3. **CMake**: Version 4.2.0 or higher.

### Build Instructions (Cross-Platform)
The project uses CMake for cross-platform compilation.
1. **Clone the Repository**
```bash
git clone https://github.com/bitlemonsoftware/cache-iq.git
```

2. **Configure the Build**
```bash
mkdir build
cd build
cmake ..
```

3. **Compile the Project**
```bash
cmake --build .
```

Upon successful compilation, the executable file will be located in the `build/bin/` folder.

## Usage
The simulator requires an input trace file and several specific parameters.

### Cache Memory Trace (.cmt) File
The trace file is a simple text file, where each line represent an instruction such as reading from memory or writing to memory.
Each line contains two inputs:
1. **Type**: The type of instruction to execute (`R` = Read from memory / `W` = Write to memory).
2. **Address**: The hexadecimal representation of the accessed memory address (in the form of `0x00000000`).
You can find a few trace file examples in the `traces/` folder.

### Parameters
1. **Trace File Path**: The path to the trace file, which contains a list of instruction that will be fed as input to the cache simulator.
2. **Cache Size (KB)**: The size of the cache in KB (Available values: `8`, `16`, `32`, `64`).
3. **Associativity**: The number of ways in the cache (Must be a power of two, minimum: 1, maximum: 1024).
4. **Replacement algorithm**: The algorithm used for replaceing cache lines (Available values: `RR` = Random Replacement, `LRU` = Least Recently Used).
5. **Output detail level**: The amount of output information (Available values: `0` = High-level cache statistics, `1` = Detailed per-instruction statistics).

### Run the Simulator
Execute the compiled application, passing the trace file path and parameters as command-line arguments:

`./CacheIQ <path_to_tracefile.cmt> <cache_size_kb> <associativity> <replacement_algorithm> <output_level>`

**Example**: To simulate a 32KB cache, 4-way associativity, Least Recentry Used replacement, and Extended output level using my_trace.cmt:

`./CacheIQ my_trace.cmt 32 4 LRU 1`

## Output
The output is written directly to the CLI and depends on the selected output detail level.
1. **Minimal**: A summary of the statistics including instruction count, miss rates, bytes transferred, etc.
2. **Extended**: Per-instruction statistics such as: type, address, tag, set index, byte offset, result, data, evicted way index, etc.
