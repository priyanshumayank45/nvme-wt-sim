# Stage 5 – Testing, Integration & Improvement

## 1. Objective

Stage 5 evaluates the implemented Write-Through Caching NVMe Accelerator Simulator using different workloads and device timing modes.

The testing compares the baseline implementation with the optimized write-through cache implementation.

The main metrics evaluated are:

- Latency
- P50/P95/P99 latency
- Maximum latency
- Physical operations
- Write coalescing
- Throughput
- IOPS
- Wall-clock execution time
- Queue utilization

---

## 2. Test Environment

- Operating System: Ubuntu on WSL
- Compiler: g++ 13.3.0
- Language: C++17
- Build system: GNU Make 4.3
- Compiler optimization: -O2
- Warning flags: -Wall -Wextra
- Threading: pthread
- NVMe queues: 8 by default
- Logical requests: 20,000 by default

---

## 3. Test 1 – Uniform Workload

The first test used the uniform workload with 20,000 logical requests.

### Results

| Metric | Baseline | Optimized |
|---|---:|---:|
| Logical requests | 20,000 | 20,000 |
| Physical operations | 20,000 | 17,205 |
| Coalescing ratio | 0% | 13.975% |
| Average latency (µs) | 3271.99 | 2637.97 |
| P50 latency (µs) | 2854.62 | 2320.89 |
| P95 latency (µs) | 5943.03 | 5200.28 |
| P99 latency (µs) | 7417.54 | 7325.87 |
| Maximum latency (µs) | 19741.8 | 26187 |
| Physical throughput (MB/s) | 8.34488 | 10.1361 |
| Application throughput (MB/s) | 8.34488 | 11.7827 |
| Application IOPS | 2136.29 | 3016.38 |
| Physical IOPS | 2136.29 | 2594.84 |
| Wall time (seconds) | 9.36203 | 6.63046 |

### Observation

The optimized implementation reduced physical operations by approximately 13.98%.

Average latency decreased and application throughput and IOPS increased.

However, the maximum observed latency increased. This indicates a possible tail-latency trade-off.

---

## 4. Test 2 – Zipf Workload

The second test used a Zipfian workload with the default skew factor.

A Zipfian workload concentrates accesses on a smaller set of frequently accessed addresses.

### Results

| Metric | Baseline | Optimized |
|---|---:|---:|
| Logical requests | 20,000 | 20,000 |
| Physical operations | 20,000 | 17,224 |
| Coalescing ratio | 0% | 13.88% |
| Average latency (µs) | 2445.05 | 1333.83 |
| P50 latency (µs) | 2311.56 | 1162.52 |
| P95 latency (µs) | 4570.13 | 2627.71 |
| P99 latency (µs) | 5652.5 | 3775.9 |
| Maximum latency (µs) | 14785.2 | 20872.9 |
| Physical throughput (MB/s) | 11.2173 | 20.1027 |
| Application throughput (MB/s) | 11.2173 | 23.3427 |
| Application IOPS | 2871.64 | 5975.73 |
| Physical IOPS | 2871.64 | 5146.3 |
| Wall time (seconds) | 6.96467 | 3.34687 |
| Average queue utilization (%) | 2.15203 | 3.85728 |

### Observation

The optimized implementation performed substantially better for the Zipf workload.

The average latency decreased by approximately 45%.

Application throughput more than doubled, increasing from approximately 11.22 MB/s to 23.34 MB/s.

Application IOPS increased from approximately 2,872 to approximately 5,976.

Physical operations decreased by approximately 13.88%.

The maximum latency increased, showing that tail latency remains an area for improvement.

---

## 5. Test 3 – Real Linux O_DIRECT I/O

The third test used:

```text
--sim-latency-us 0
