# Stage 5 — Testing and Integration

## 1. Objective

The objective of Stage 5 is to test the Write-Through Caching NVMe Accelerator Simulator under different workloads and configurations.

The testing focuses on:

- correctness of logical and physical write operations
- write coalescing
- latency
- throughput
- IOPS
- queue utilization
- effect of workload distribution
- effect of cache tuning parameters
- comparison between baseline and optimized execution

The simulator is a user-space NVMe/device-behavior simulator. It models NVMe-style queues and device behavior using Linux system programming and C++.

---

## 2. Test Environment

- Operating System: Ubuntu under WSL
- Compiler: g++ 13.3.0
- C++ Standard: C++17
- Build system: Make
- Workload size: 20,000 logical write requests
- Address space: 50,000 blocks
- NVMe queues: 8
- Application threads: 8
- Random seed: 42

Two execution modes are compared:

### Baseline

Each logical write is submitted directly to the simulated NVMe device.

### Optimized

Writes are first collected by the write-through cache and then flushed in batches to multiple NVMe-style queues.

---

# 3. Test 1 — Uniform Workload

Command:

```bash
./nvme_wt_sim --distribution uniform
o

