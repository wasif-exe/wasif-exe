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

#### 1. [Wire v6 — Asynchronous Smart-Node Infrastructure Appliance](https://github.com/wasif-exe/wire)
> **A zero-syscall, hardware-vectorized kernel-bypass network appliance with QUIC/HTTP3, AVX-512 parsing, io_uring SQPOLL NVMe, and a Thread-per-Core async runtime in Rust.**
* **Zero-Copy QUIC + HTTP/3 Engine:** From-scratch RFC 9000 state machine over AF_XDP UMEM rings, TLS 1.3 key derivation (HKDF-SHA256), AES-128-GCM payload crypto, and RFC 9204 QPACK at **13.22 Mops/s encode / 6.20 Mops/s decode**.
* **AVX-512 Universal Dataplane:** Dual-stack IPv4/IPv6 L2-L4 parser with branchless extension-header traversal and CPUID dispatch (AVX-512 -> AVX2 -> Scalar). Scalar path hits **75.43 Mpps**; SmartNIC offload hints drop checksum cost to **2.88 cycles/pkt** (226 cycles saved).
* **io_uring SQPOLL NVMe Reactor:** Kernel submission polling + fixed registered buffers (`IORING_REGISTER_BUFFERS`) delivering **2,169.76 MB/s** Direct I/O and **25.28 Mops/s** async WAL at **42.10 ns** submission overhead.
* **Thread-per-Core Async Runtime:** Shared-nothing, CPU-pinned `LocalExecutor` with custom `RawWakerVTable` at **202.15 Mops/s** task dispatch (**4.95 ns/task**). No Arc, no Mutex, no work-stealing on the hot path.
* **Hardware-Sympathetic Foundation:** AF_XDP 2MB HugePage UMEM, eBPF selective flow bridge, Google BBR + RFC 6675 SACK, flat slab ConnTable, lock-free 4-tier timing wheel, and 300-seed deterministic chaos verification.

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
  <img src="https://github-stats-extended.vercel.app/api?username=wasif-exe&show_icons=true&theme=dark&hide_border=true" alt="Wasif's GitHub Stats" height="165" />
  <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=wasif-exe&layout=compact&theme=dark&hide_border=true&hide=html,css,php" alt="Top Languages" height="165" />
</p>

---

<p align="center">
  <i>"In low-latency systems, you aren't racing other developers. You are negotiating with cache lines, CPU branch predictors, and the speed of light."</i>
</p>
