<div align="center">

# SYED WASIF

**Systems Software Engineer · Kernel-Bypass Infrastructure · Low-Latency Architecture**

[![Portfolio](https://img.shields.io/badge/Portfolio-Visit_Site-005599?style=for-the-badge&logo=vercel&logoColor=white)](https://wasif-exe.me/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-wasif--exe-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/wasif-exe)
[![X / Twitter](https://img.shields.io/badge/X-@wasif__exe-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/wasif_exe)
[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:syedwasifzidane@gmail.com)

---

### Technical Stack & Core Domain

| Domain | Technologies & Architectural Focus |
| :--- | :--- |
| **Languages** | `Rust` · `C` · `C++20` · `x86_64 Assembly` · `Huff EVM Assembly` · `Python` · `Bash` |
| **Systems & Kernel** | `Linux 6.x` · `AF_XDP (XSK)` · `eBPF / XDP` · `2MB HugePages (MAP_HUGETLB)` · `io_uring (SQPOLL + REGISTER_BUFFERS)` · `Direct I/O (O_DIRECT \| O_DSYNC)` · `mmap` · `POSIX` · `TAP` · `sched_setaffinity` |
| **Networking & Protocols** | `RFC 9000 (QUIC)` · `RFC 9001 (QUIC-TLS)` · `RFC 9114 (HTTP/3)` · `RFC 9204 (QPACK)` · `RFC 9293 (TCP)` · `Google BBR` · `RFC 6675 SACK` · `RFC 8200 (IPv6)` · `RESP v2 (Redis)` · `TLS 1.3` · `ARP` · `DNS` · `ICMP` |
| **Concurrency & Memory** | `Thread-per-Core (TxC)` · `Shared-Nothing Executors` · `Lock-Free Atomics` · `Flat Slab Allocators` · `SPSC / MPMC Rings` · `Vyukov Queues` · `EBR Reclamation` · `align(64)` · `mimalloc` · `Custom RawWakerVTable` |
| **Hardware & Performance** | `rdtsc Cycle Profiling` · `x86_64 AVX-512 / AVX2 SIMD` · `SSE4.2 CRC32C` · `AES-128-GCM / HKDF-SHA256` · `SmartNIC Metadata Offload` · `Word-Parallel Checksums` · `Cache Line Alignment` · `Fat LTO` |
| **Verification & Tools** | `Deterministic Simulation Testing (DST)` · `Loom` · `ThreadSanitizer` · `perf` · `strace` · `Valgrind` · `GDB` · `CPUID Feature Dispatch` |

<br/>

<p align="center">
  <img src="https://skillicons.dev/icons?i=rust,cpp,c,linux,python,bash,docker,git" alt="Tech Stack" />
</p>

---

### Featured Systems Flagships

#### 1. [Wire v9 — Zero-Allocation Matching Engine & Memory Kernel](https://github.com/wasif-exe/wire)
> **A 24-crate from-scratch HFT stack spanning full TCP/IP, kernel bypass, VFIO PCIe DMA, SIMD parsing, a flat-array matching engine, HugePage slab allocator, and lock-free MPMC queues in Rust and C.**
* **Flat-Array Matching Engine:** Price-time priority order book with O(1) price lookup via direct array indexing (`[PriceLevel; 65536]`), 16-byte cache-aligned `OrderSlot` structs (4 per cache line), and bounded best-bid/ask watermark scans. Core match loop at **11.20 cycles (3.7 ns)** per fill, **267.8 Mops/s**.
* **HugePage Memory Kernel:** Thread-local slab allocator with 64/128/256B fixed size classes backed by 1GB HugePages (2MB/4KB fallback) via intrusive free lists. Alloc+free at **1.55 ns (646.4 Mops/s)**. Paired with a Vyukov-style lock-free MPMC bounded queue at **6.52 ns push+pop (153.3 Mops/s)** with `align(64)` cursor isolation.
* **AVX2 Batch Order Cancellation:** Vectorized 8-wide order slot scanning using `_mm256_cmpeq_epi32` (user cancel) and `_mm256_cmpgt_epi32` (price sweep) on `align(32)` packed arrays. **0.96 cycles per 8 slots (24,892 Mslots/s)** for user-ID matching, **0.95 cycles** for price threshold sweeps.
* **Bare-Metal Hardware Dataplane:** VFIO PCIe BAR0 MMIO doorbell writes at **0.90 ns/tx**, CME MDP 3.0 Little-Endian SBE decoding at **3.45 cycles/msg (870 Mpps)**, dual-feed A/B multicast arbitration at **4.41 cycles**, POSIX `LD_PRELOAD` socket shim at **10.64 cycles/call**, and PTP PI clock servo.
* **Full-Stack Foundation (v1–v8):** From-scratch TCP/IP with PAWS/SACK/BBR, AF_XDP zero-copy UMEM rings, QUIC/HTTP3 with TLS 1.3 (AES-128-GCM + HKDF-SHA256), AVX-512 dual-stack L2-L4 parser, `io_uring` SQPOLL NVMe reactor (**2.17 GB/s**), eBPF XDP pre-trade risk filter, and 300-seed deterministic chaos verification.

#### 2. [Thread-Per-Core io_uring & LSM-Tree Storage Engine](https://github.com/wasif-exe/lsm-engine)
> **A zero-dependency, 3-tier database engine built from raw Linux 6.x kernel primitives up to NVMe persistence.**
* **Kernel-Bypass Networking:** Thread-per-core event loop using `recv_MULTISHOT` and kernel-provided buffer rings (`PBUF_RING`), cutting steady-state syscalls by **80.1%** compared to multi-threaded `epoll` (300k+ req/sec).
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
  <img src="https://komarev.com/ghpvc/?username=wasif-exe&label=PROFILE+VIEWS&color=005599&style=for-the-badge" alt="Profile Views" />
</p>

<p align="center">
  <img src="https://github-stats-extended.vercel.app/api?username=wasif-exe&show_icons=true&theme=dark&hide_border=true" alt="Wasif's GitHub Stats" height="165" />
  <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=wasif-exe&layout=compact&theme=dark&hide_border=true&hide=html,css,php" alt="Top Languages" height="165" />
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=wasif-exe&theme=dark&hide_border=true" alt="GitHub Streak" height="165" />
</p>



<p align="center">
  <i>"In low-latency systems, you aren't racing other developers. You are negotiating with cache lines, CPU branch predictors, and the speed of light."</i>
</p>
