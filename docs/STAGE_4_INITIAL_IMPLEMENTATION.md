# Stage 4 – Initial Implementation & Prototype

## 1. Objective

The objective of Stage 4 is to implement and validate the initial prototype of the Write-Through Caching NVMe Accelerator Simulator.

The prototype models an NVMe-style storage system in user space using C++17 and Linux system programming concepts.

## 2. Development Environment

- Operating System: Ubuntu on WSL
- Compiler: g++ 13.3.0
- Build Tool: GNU Make 4.3
- Language: C++17
- Build flags: -O2 -Wall -Wextra -pthread
- Architecture: x86-64 Linux

## 3. Initial Implementation

The prototype contains the following major components:

- Workload generation
- Write-through cache
- NVMe device simulation
- Multiple NVMe-style queues
- Request processing using worker threads
- Metrics collection
- Baseline and optimized execution modes
- Result generation in CSV format
- Performance charts and execution logs

## 4. Prototype Build

The project was successfully compiled using:

```bash
make clean
make
