<div align="center">

# SYED M WASIF

**Systems Software Engineer · Low-Latency Infrastructure · Kernel-Bypass Architectures**

[![Portfolio](https://img.shields.io/badge/Portfolio-Visit_Site-005599?style=for-the-badge&logo=vercel&logoColor=white)](https://wasif-exe.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-wasif--exe-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/wasif-exe)
[![X / Twitter](https://img.shields.io/badge/X-@wasif__exe-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/wasif_exe)
[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:syedwasifzidane@gmail.com)

</div>

---

### ⚡ Verified Benchmark Highlights

```text
┌──────────────────────────────────────────────────────────────────────────────────────┐
│  • Decision Latency  :  37 ns / tick (0.5M mainnet candidates evaluated in 18.5ms)   │
│  • Network Engine    :  300,619 req/sec on 4 physical cores (80.1% syscall drop)     │
│  • Storage Engine    :  2.13M ops/sec MemTable inserts · 1.88x Compaction WAF        │
│  • Hardware Vector   :  1.27M ops/sec point reads via AVX2 SIMD Bloom probes         │
└──────────────────────────────────────────────────────────────────────────────────────┘
```

---

### 🛠️ Technical Stack & Core Domain

| Domain | Technologies & Hardware Focus |
| :--- | :--- |
| **Languages** | `Rust` · `C` · `C++20` · `x86_64 Assembly` · `Huff EVM Assembly` · `Python` · `Bash` |
| **Systems & Kernel** | `Linux 6.x` · `io_uring (PBUF_RING, MULTISHOT)` · `Direct I/O (O_DIRECT)` · `mmap` · `POSIX` |
| **Concurrency & Memory** | `Lock-Free Atomics` · `Vyukov MPMC Queues` · `EBR Reclamation` · `align(64)` · `mimalloc` |
| **Hardware & Performance** | `x86_64 AVX2 SIMD` · `Cache Line Alignment` · `L1/L2 Cache Optimization` · `LTO` |
| **Verification & Profiling** | `Loom (Model Checking)` · `ThreadSanitizer` · `gdb` · `perf` · `strace` · `Valgrind` |

<br/>

<p align="center">
  <img src="https://skillicons.dev/icons?i=rust,cpp,c,linux,python,bash,docker,git" alt="Tech Stack" />
</p>

---

### 🚀 Featured Architectural Systems

#### 1. [Thread-Per-Core io_uring & LSM-Tree Storage Engine](https://github.com/wasif-exe)
> **A zero-dependency, 3-tier database engine built from raw Linux 6.x kernel primitives up to NVMe persistence.**
* **Kernel-Bypass Network:** Thread-per-core event loop using `RECV_MULTISHOT` and kernel-provided buffer rings (`PBUF_RING`), cutting steady-state syscalls by **80.1%** compared to multi-threaded `epoll` (300k+ req/sec).
* **Lock-Free Concurrency:** Custom Vyukov MPMC queue and 3-epoch Epoch-Based Reclamation (EBR) collector with `align(64)` cache-line isolation. Formally verified for race freedom via **Loom** state-space model checking and **ThreadSanitizer**.
* **Storage & SIMD Engine:** `O_DIRECT` sector-aligned WAL, lock-free SkipList MemTable (**2.13M ops/sec**), `mmap` SSTables (**1.88x WAF**), and **x86_64 AVX2 SIMD-vectorized** Bloom filter probes (**1.27M ops/sec** point reads).

#### 2. [Mark V — 37ns Ultra-Low-Latency Decision Engine](https://github.com/wasif-exe)
> **A deterministic, zero-allocation in-memory mempool evaluation engine engineered for extreme low-latency execution.**
* **Tick Latency:** Achieved a **37 ns / tick** (~185 CPU cycles at 5 GHz) average decision latency over **490,444 historical mainnet candidates** (0.5M candidates in 18.5ms total wall time).
* **Mechanical Sympathy:** Zero heap allocations, zero string hashing, and zero floats in the hot path. Built using `align(64)` POD candidate structures, `FxHashMap` integer lookups, `mimalloc`, and native fat LTO binary compilation.
* **Offline Precision:** **99.89%** floor coverage, **98%** precision, and **1.00** recall on historical execution replay.

#### 3. [Project Iron Lung — High-Throughput Arbitrage Scout & MEV Framework](https://github.com/wasif-exe)
> **A low-latency EVM reconnaissance and execution framework targeting Base L2.**
* Ingress signature filtering analyzing 4-byte EVM selectors to shed **90%+ of non-arbitrage network noise**.
* OS-level thread scheduler prioritization (`nice -n -20`) to eliminate context-switch latency spikes during block ingestion.
* Custom smart execution contracts authored in **Huff EVM Assembly** and **Rust**.

#### 4. [Neural Wasif — Autonomous Multi-Agent Personal AI OS](https://github.com/wasif-exe)
> **An autonomous, multi-agent AI operating system deployed on an ARM64 edge node.**
* Zero-downtime multi-provider LLM router dynamically switching across cloud APIs based on rate limits, latency, and capability state.
* 5-mode cognitive state machine featuring heuristic safety interception for shell execution and RAG-driven persona style-cloning across 18k+ chat turns.

---

### 📊 GitHub Activity

<p align="center">
  <img src="https://github-stats-extended.vercel.app/api?username=wasif-exe&show_icons=true&theme=dark&hide_border=true" alt="Wasif's GitHub Stats" height="165" />
  <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=wasif-exe&layout=compact&theme=dark&hide_border=true&hide=html,css,php" alt="Top Languages" height="165" />
</p>

---

<p align="center">
  <i>"In low-latency systems, you aren't racing other developers — you are negotiating with cache lines, CPU branch predictors, and the speed of light."</i>
</p>
