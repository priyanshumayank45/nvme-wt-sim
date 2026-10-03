# Stage 3 – System Design & Architecture

## 1. Project Title

Write-Through Caching NVMe Accelerator Simulator using Linux and C++

---

## 2. System Overview

The system is a Linux-based C++17 simulator that models write-through caching and NVMe-style storage processing.

The system contains a workload generator, application threads, a write-through cache, NVMe-style queues, an NVMe device simulator, Linux storage I/O, and a metrics collection system.

The architecture supports two implementations:

1. Baseline write-through cache
2. Optimized write-through cache

The optimized implementation introduces concurrent processing, multiple queues, batching, and write coalescing.

---

# 3. High-Level Architecture

```text
+---------------------------+
|     Workload Generator    |
+-------------+-------------+
              |
              | Write Requests
              v
+---------------------------+
|    Application Threads    |
+-------------+-------------+
              |
              v
+---------------------------+
|    Write-Through Cache   |
|                           |
|  Baseline / Optimized     |
+-------------+-------------+
              |
              | Pending Writes
              v
+---------------------------+
|    NVMe Queue Manager     |
+------+------+------+------+
       |      |      |
       v      v      v
    Queue0 Queue1 Queue2 ... QueueN
       |      |      |
       +------+------+ 
              |
              v
+---------------------------+
|   NVMe Device Simulator   |
+-------------+-------------+
              |
              | Linux I/O
              v
+---------------------------+
|      Backing Storage      |
|          File             |
+---------------------------+

              |
              v
+---------------------------+
|       Metrics Module      |
+-------------+-------------+
              |
              v
+---------------------------+
|    CSV / Result Output    |
+---------------------------+
