
<div align="center">

# SYED WASIF

**Systems Software Engineer · Kernel-Bypass Infrastructure · Low-Latency Architecture**

[![Portfolio](https://img.shields.io/badge/Portfolio-Visit_Site-005599?style=for-the-badge&logo=vercel&logoColor=white)](https://wasif-exe.me/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-wasif--exe-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/wasif-exe)
[![X / Twitter](https://img.shields.io/badge/X-@wasif__exe-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/wasif_exe)
[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:syedwasifzidane@gmail.com)

---

### Verified Benchmark Receipts & Systems Metrics

```text
┌───────────────────────────────────────────────────────────────────────────────────┐
│  • Multi-Core Sharding : 165.57 Mpps aggregate rate across 4 shared-nothing cores │
│  • L7 Storage Performance: 7.29 Million ops/sec zero-copy Redis RESP v2 server    │
│  • Hardware Vectoring  : 10.25 Gbps single-core checksum · 31.15 ns BBR pacing    │
│  • Storage Engine      : 2.13M ops/sec MemTable · 1.88x Compaction WAF            │
│  • Kernel Bypass       : 300,619 req/sec on 4 physical cores (80.1% syscall drop) │
│  • Decision Engine     : 37 ns / tick avg (0.5M candidates evaluated in 18.5ms)   │
│  • Consensus Sim       : ~397,000 ticks/sec deterministic verification harness    │
└───────────────────────────────────────────────────────────────────────────────────┘
```

</div>

---

### Technical Stack & Core Domain

| Domain | Technologies & Architectural Focus |
| :--- | :--- |
| **Languages** | `Rust` · `C` · `C++20` · `x86_64 Assembly` · `Huff EVM Assembly` · `Python` · `Bash` |
| **Systems & Kernel** | `Linux 6.x` · `AF_XDP (XSK)` · `eBPF` · `2MB HugePages (MAP_HUGETLB)` · `Direct I/O (O_DIRECT)` · `io_uring` · `mmap` · `POSIX` · `TAP` |
| **Networking & Protocols** | `RFC 9293 (TCP)` · `Google BBR` · `RFC 6675 SACK` · `RESP v2 (Redis)` · `TLS 1.3` · `ARP` · `DNS` · `ICMP` |
| **Concurrency & Memory** | `Lock-Free Atomics` · `Flat Slab Allocators` · `Vyukov MPMC Queues` · `EBR Reclamation` · `align(64)` · `mimalloc` |
| **Hardware & Performance** | `rdtsc Cycle Profiling` · `Word-Parallel Checksums` · `x86_64 AVX2 SIMD` · `Cache Line Alignment` · `Fat LTO` |
| **Verification & Tools** | `Deterministic Simulation Testing (DST)` · `Loom` · `ThreadSanitizer` · `perf` · `strace` · `Valgrind` · `GDB` |

<br/>

<p align="center">
  <img src="https://skillicons.dev/icons?i=rust,cpp,c,linux,python,bash,docker,git" alt="Tech Stack" />
</p>

---

### Featured Systems Flagships

#### 1. [Wire v4 — Hardware-Sympathetic AF_XDP Dataplane & Redis Engine](https://github.com/wasif-exe/wire)
> **A zero-syscall, 165 Mpps bare-metal network stack & AF_XDP kernel-bypass engine in Rust.**
* **Hardware-Sympathetic Memory:** Replaced pointer-chasing heap objects with a flat `ConnTable` slab allocator and 2MB HugePages (`MAP_HUGETLB` + `mlock`), dropping UMEM TLB page entries from 2048 to **4**.
* **Shared-Nothing Multi-Core Sharding:** 4-tuple flow-steering hash map distributing packets across CPU-pinned workers without locks or atomics (**165.57 Mpps aggregate classification rate**).
* **`rdtsc` Stage Profiling & BBR:** Instrumenting pipeline stages via hardware cycle counters (L2-L4 parse ~3300 cycles; BBR pacing barrier **31.15 ns/eval**).
* **L7 Redis KV Engine (`wire-redis`):** Zero-copy RESP v2 streaming parser serving **7.29 Million ops/sec** (~137.2 ns/op), verified compatible with `redis-cli` and `valkey-cli`.

#### 2. [Thread-Per-Core io_uring & LSM-Tree Storage Engine](https://github.com/wasif-exe/lsm-engine)
> **A zero-dependency, 3-tier database engine built from raw Linux 6.x kernel primitives up to NVMe persistence.**
* **Kernel-Bypass Networking:** Thread-per-core event loop using `RECV_MULTISHOT` and kernel-provided buffer rings (`PBUF_RING`), cutting steady-state syscalls by **80.1%** compared to multi-threaded `epoll` (300k+ req/sec).
* **Lock-Free Concurrency:** Custom Vyukov MPMC queue and 3-epoch Epoch-Based Reclamation (EBR) collector with `align(64)` cache-line isolation. Formally verified for race freedom via **Loom** model checking and **ThreadSanitizer**.
* **Storage & SIMD Engine:** `O_DIRECT` sector-aligned WAL, lock-free SkipList MemTable (**2.13M ops/sec**), `mmap` SSTables (**1.88x WAF**), and **x86_64 AVX2 SIMD-vectorized** Bloom filter probes (**1.27M ops/sec** point reads).

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

### GitHub Activity

<p align="center">
  <img src="https://github-stats-extended.vercel.app/api?username=wasif-exe&show_icons=true&theme=dark&hide_border=true" alt="Wasif's GitHub Stats" height="165" />
  <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=wasif-exe&layout=compact&theme=dark&hide_border=true&hide=html,css,php" alt="Top Languages" height="165" />
</p>

---

<p align="center">
  <i>"In low-latency systems, you aren't racing other developers — you are negotiating with cache lines, CPU branch predictors, and the speed of light."</i>
</p>
```
