
<div align="center">

# SYED WASIF

**Systems Software Engineer · Low-Latency Infrastructure · Distributed Systems & Kernel Primitives**

[![Portfolio](https://img.shields.io/badge/Portfolio-Visit_Site-005599?style=for-the-badge&logo=vercel&logoColor=white)](https://wasif-exe.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-wasif--exe-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/wasif-exe)
[![X / Twitter](https://img.shields.io/badge/X-@wasif__exe-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/wasif_exe)
[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:syedwasifzidane@gmail.com)

---

###  Benchmark Receipts & Systems Metrics

```text
┌───────────────────────────────────────────────────────────────────────────────────┐
│  • Storage Engine   : 2.13M ops/sec MemTable · 1.88x Compaction WAF               │
│  • Network Kernel   : 300,619 req/sec on 4 physical cores (80.1% syscall drop)    │
│  • Decision Engine  : 37 ns / tick avg (0.5M candidates evaluated in 18.5ms)      │
│  • Consensus Sim    : ~397,000 ticks/sec deterministic verification harness       │
│  • Userspace TCP    : Passes 300/300 chaos seeds (5% loss, 2% duplication)        │
└───────────────────────────────────────────────────────────────────────────────────┘

```

---

###  Technical Stack & Core Domain

| Domain | Technologies & Architectural Focus |
| --- | --- |
| **Languages** | `Rust` · `C` · `C++20` · `x86_64 Assembly` · `Huff EVM Assembly` · `Python` · `Bash` |
| **Systems & Kernel** | `Linux 6.x` · `io_uring (PBUF_RING, MULTISHOT)` · `Direct I/O (O_DIRECT)` · `mmap` · `POSIX` · `TAP` |
| **Concurrency & Memory** | `Lock-Free Atomics` · `Vyukov MPMC Queues` · `EBR Reclamation` · `align(64)` · `mimalloc` |
| **Networking & Protocols** | `RFC 9293 (TCP)` · `RFC 793` · `Reno Congestion` · `Jacobson/Karels RTO` · `Zero-Copy Sockets` |
| **Hardware & Performance** | `x86_64 AVX2 SIMD` · `Cache Line Alignment` · `L1/L2 Cache Optimization` · `LTO` |
| **Verification & Profiling** | `Deterministic Simulation Testing (DST)` · `Loom` · `ThreadSanitizer` · `perf` · `strace` |

---

###  Featured Systems Flagships

#### 1. [Thread-Per-Core io_uring & LSM-Tree Storage Engine](https://github.com/wasif-exe/lsm-engine)

> **A zero-dependency, 3-tier database engine built from raw Linux 6.x kernel primitives up to NVMe persistence.**

* **Kernel-Bypass Networking:** Thread-per-core event loop using `RECV_MULTISHOT` and kernel-provided buffer rings (`PBUF_RING`), cutting steady-state syscalls by **80.1%** compared to multi-threaded `epoll` (300k+ req/sec).
* **Lock-Free Concurrency:** Custom Vyukov MPMC queue and 3-epoch Epoch-Based Reclamation (EBR) collector with `align(64)` cache-line isolation. Formally verified for race freedom via **Loom** model checking and **ThreadSanitizer**.
* **Storage & SIMD Engine:** `O_DIRECT` sector-aligned WAL, lock-free SkipList MemTable (**2.13M ops/sec**), `mmap` SSTables (**1.88x WAF**), and **x86_64 AVX2 SIMD-vectorized** Bloom filter probes (**1.27M ops/sec** point reads).

#### 2. [Wire — Userspace TCP/IP Stack & Zero-I/O Protocol Engine](https://github.com/wasif-exe/wire)

> **A zero-syscall, RFC 9293 compliant TCP/IP stack implemented from scratch in Rust over Linux TAP devices.**

* **Full Protocol State Machine:** Implements the complete 11-state TCP FSM, completing 3-way handshakes with the live Linux kernel, handling active HTTP/1.1 client opens, and verifying 1MB transfers via byte-perfect SHA-256 hashes.
* **Congestion & RTO Engine:** Features TCP Reno congestion control, Jacobson/Karels RTO estimation, Karn's algorithm, and sequence number wraparound arithmetic.
* **Chaos Verification:** Pure zero-I/O deterministic state machine passing **300/300 chaos seeds** under simulated 5% packet loss, 2% packet duplication, and network jitter.

#### 3. [Raft-₹ — Pure Consensus Kernel & Deterministic Chaos Simulator](https://github.com/wasif-exe/raft-rupee)

> **An I/O-free Raft consensus kernel powered by seed-driven deterministic simulation testing.**

* **Pure State Machine (`raft-core`):** Zero threads, zero async runtimes, zero sockets. Pure deterministic execution driven strictly by `tick() -> Vec<Action>` and `step(msg) -> Vec<Action>`.
* **Deterministic Chaos Harness (`raft-sim`):** Evaluates Election, Log Matching, and State Machine safety invariants across simulated network partitions, packet drops, and node crashes at **~397,000 ticks/sec**.
* **Production Runtime (`raft-server`):** Driven by `O_DIRECT` + `O_DSYNC` 4096-byte sector-aligned physical disk writes with CRC32 integrity, Pre-Vote protocol (§9.6), and strict Figure 8 commitments (§5.4.2).

#### 4. [Mark V — 37ns Ultra-Low-Latency Decision Engine](https://www.linkedin.com/posts/wasif-exe_rustlang-lowlatency-systemsengineering-activity-7502939036270092289-0vuR)

> **A deterministic, zero-allocation in-memory mempool evaluation engine engineered for extreme low-latency execution.**

* **Tick Latency:** Achieved a **37 ns / tick** (~185 CPU cycles at 5 GHz) average decision latency over **490,444 historical mainnet candidates** (0.5M candidates in 18.5ms total wall time).
* **Mechanical Sympathy:** Zero heap allocations, zero string hashing, and zero floats in the hot path. Built using `align(64)` POD candidate structures, `FxHashMap` integer lookups, `mimalloc`, and native fat LTO binary compilation.
* **Offline Precision:** **99.89%** floor coverage, **98%** precision, and **1.00** recall on historical execution replay.

---

###  GitHub Activity


<p align="center"> <img src="https://github-stats-extended.vercel.app/api?username=wasif-exe&show_icons=true&theme=dark&hide_border=true" alt="Wasif's GitHub Stats" height="165" /> <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=wasif-exe&layout=compact&theme=dark&hide_border=true&hide=html,css,php" alt="Top Languages" height="165" /> </p>
