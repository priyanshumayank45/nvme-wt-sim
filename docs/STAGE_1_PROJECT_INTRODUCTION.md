# Stage 1 – Project Introduction

## Project Title

Write-Through Caching NVMe Accelerator Simulator using Linux and C++

## 1. Introduction

NVMe storage devices are designed to support high-performance and parallel input/output operations using multiple queues.

A simple write-through caching system may process storage write requests sequentially. This can limit the amount of parallelism that can be utilized by the storage system.

This project develops a Linux-based C++ simulator to study write-through caching and NVMe-style queue processing. The project compares a baseline write-through cache with an optimized implementation using concurrency, multiple queues, batching, and write coalescing.

The project uses Linux system-level file I/O mechanisms and modern C++ programming techniques to model storage operations and measure system performance.

## 2. Problem Statement

A basic write-through cache sends every write request to the underlying storage and waits for the storage operation to complete.

When requests are processed sequentially, the available parallelism of NVMe-style storage may not be fully utilized.

The project aims to investigate whether multiple queues, concurrent processing, batching, and write coalescing can improve storage-write performance while maintaining write-through behavior.

## 3. Objectives

The main objectives of the project are:

1. Implement a baseline write-through cache.
2. Implement an optimized write-through cache.
3. Simulate multiple NVMe-style submission/completion queues.
4. Use Linux system programming interfaces for storage operations.
5. Use C++17 for implementation.
6. Support concurrent application write requests.
7. Implement batching and write coalescing.
8. Generate configurable storage workloads.
9. Measure latency and throughput.
10. Measure IOPS and physical storage operations.
11. Compare baseline and optimized implementations.
12. Analyze the performance differences between the two approaches.

## 4. Project Scope

The project covers:

- Linux system programming
- C++17 programming
- File-based storage simulation
- NVMe queue concepts
- Write-through caching
- Multithreading
- Synchronization
- Direct I/O
- Workload generation
- Performance measurement
- Result analysis

The project models NVMe-style behavior in user space. It does not replace the Linux kernel's actual NVMe driver.

## 5. Expected Outcome

The expected outcome is a working Linux-based C++ simulator capable of:

- Processing write requests.
- Simulating NVMe-style queues.
- Performing concurrent write operations.
- Applying write-through caching.
- Performing write batching.
- Coalescing repeated writes where applicable.
- Measuring system performance.
- Producing results for comparison between baseline and optimized implementations.

## 6. Application

The project can be used as an educational and experimental platform for understanding:

- Storage systems
- NVMe architecture
- Linux I/O
- C++ concurrency
- Cache management
- Performance optimization
- System-level programming

The simulator can also be extended in the future to study additional storage scheduling and caching techniques.

## 7. Technologies Used

| Technology | Purpose |
|---|---|
| Ubuntu/Linux | Development and execution environment |
| C++17 | Core implementation |
| Linux system calls | Storage I/O |
| POSIX APIs | Low-level system interaction |
| Multithreading | Concurrent request processing |
| Make | Build automation |
| Git | Version control |
| GitHub | Source-code repository |
| Python | Result visualization |

## 8. Expected Deliveables

The project will produce:

- C++ source code
- Header files
- Build configuration
- Workload generator
- Performance measurement module
- Result visualization scripts
- Documentation
- UML diagrams
- Test results
- Performance comparison
- GitHub repository
- Final project report
