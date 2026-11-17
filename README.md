# Mohamed Hamed

** Java & Systems Concurrency Engineer | High-Throughput Enterprise Backend & Systems Internals**  
*M.Sc. Software Architecture @ Eötvös Loránd University (ELTE)*  
Budapest, Hungary • [LinkedIn](https://www.linkedin.com/in/mohameddhamed/) • [GitHub](https://github.com/mohameddhamed)

[![Java 21](https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Rust](https://img.shields.io/badge/Rust-1.80%2B-DEA584?logo=rust&logoColor=black)](https://www.rust-lang.org/)
[![C++20](https://img.shields.io/badge/C%2B%2B-20-00599C?logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
[![Go](https://img.shields.io/badge/Go-1.22%2B-00ADD8?logo=go&logoColor=white)](https://go.dev/)

---

## 🛠️ Engineering Profile

I am a **Senior Java & Systems Concurrency Engineer** with 3.5+ years of continuous enterprise backend experience engineering core database platforms, mission-critical microservices, and distributed runtime systems:

- **Enterprise Java & High-Concurrency Systems:** Architected and scaled high-throughput enterprise backend services utilizing **Java 21**, **Spring Boot**, and **Project Loom (Virtual Threads)**. Specialized in high-concurrency request pipelining, non-blocking asynchronous architectures, JVM garbage collection tuning, carrier thread starvation prevention, and synchronized monitor pinning mitigation.
- **SAP (Core Platform & In-Memory Database Internals):** Engineered internal storage and query execution layers for **SAP HANA TableStore**, focusing on in-memory columnar layouts, dictionary compression, SIMD vectorized filter pushdown, and direct-indexed zero-hash-table grouping.
- **ExxonMobil (Distributed Systems & Services):** Designed and deployed resilient enterprise distributed logging pipelines, event-driven microservices, and high-throughput data ingestion middleware serving global operations.
- **Low-Latency & Systems Infrastructure:** Built zero-allocation trading runtimes, asynchronous LSM-tree storage engines, and ahead-of-time compilers across **Rust**, **Modern C++ (C++20)**, and **Go**.

---

## 🏛️ Flagship Showcase (Core Pillars)

| System / Repository | Primary Stack | Domain / Focus | Key Architectural Highlights | CI / Verification |
| :--- | :--- | :--- | :--- | :---: |
| **[virtual-thread-springs](https://github.com/mohameddhamed/virtual-thread-springs)** | **Java 21**, Spring Boot | JVM Concurrency & Virtual Threads | Project Loom empirical research: carrier thread starvation, synchronized monitor pinning mitigation, non-blocking concurrency | ![Research](https://img.shields.io/badge/Research-M.Sc._Thesis-blue.svg) |
| **[aetherkv](https://github.com/mohameddhamed/aetherkv)** | **Rust**, `io_uring`, AVX2 | Asynchronous LSM Storage Engine | Lock-free MemTable with bump arena, inode-free pre-allocated Direct I/O WAL, 4KB delta SSTables & AVX2 Bloom filters | [![CI](https://github.com/mohameddhamed/aetherkv/actions/workflows/ci.yml/badge.svg)](https://github.com/mohameddhamed/aetherkv/actions/workflows/ci.yml) |
| **[nexusloop](https://github.com/mohameddhamed/nexusloop)** | **C++20**, SIMD, `io_uring` | Low-Latency Trading Gateway | Zero-allocation trading runtime, lock-free Disruptor ring buffers, cache-line isolation, SIMD ITCH 5.0 order parser | [![CI](https://github.com/mohameddhamed/nexusloop/actions/workflows/ci.yml/badge.svg)](https://github.com/mohameddhamed/nexusloop/actions/workflows/ci.yml) |
| **[mini-columnar-engine](https://github.com/mohameddhamed/mini-columnar-engine)** | **Rust**, Vectorized OLAP | In-Memory Database Internals | Morsel-driven chunked execution mirroring SAP HANA TableStore, dictionary encoding, SIMD slice matching (3.96B elem/s) | [![CI](https://github.com/mohameddhamed/mini-columnar-engine/actions/workflows/ci.yml/badge.svg)](https://github.com/mohameddhamed/mini-columnar-engine/actions/workflows/ci.yml) |
| **[resp-storage-engine](https://github.com/mohameddhamed/resp-storage-engine)** | **Go**, Redis RESP2 | Concurrent In-Memory KV Store | Zero-allocation byte builders, fine-grained `sync.RWMutex`, isolated transactions (`MULTI`/`EXEC`), master-replica replication | [![CI](https://github.com/mohameddhamed/resp-storage-engine/actions/workflows/ci.yml/badge.svg)](https://github.com/mohameddhamed/resp-storage-engine/actions/workflows/ci.yml) |
| **[while-x86-compiler](https://github.com/mohameddhamed/while-x86-compiler)** | **C++**, x86 Assembly | Ahead-of-Time (AOT) Compiler | Flex/Bisonc++ LALR(1) front-end, AST semantic analysis, 32-bit x86 NASM code generator, standard C ABI bridge (`cdecl`) | [![CI](https://github.com/mohameddhamed/while-x86-compiler/actions/workflows/ci.yml/badge.svg)](https://github.com/mohameddhamed/while-x86-compiler/actions/workflows/ci.yml) |

---

## 🔬 Deep-Dive Project Breakdowns

### 1. [virtual-thread-springs](https://github.com/mohameddhamed/virtual-thread-springs) (Java 21, Spring Boot)
*M.Sc. thesis research application and empirical benchmark study on Java 21 Project Loom virtual thread mechanics.*
- **Concurrency & Carrier Starvation:** Measures throughput degradation and carrier thread saturation under intensive MVC request patterns, identifying carrier thread starvation thresholds.
- **Monitor Pinning Analysis:** Evaluates Java 21 runtime behavior where virtual threads become pinned to carrier OS threads inside `synchronized` blocks or native methods, converting non-blocking cooperative fibers into blocking bottlenecks.
- **Safe Concurrency Refactoring:** Implements production-ready migration patterns replacing legacy synchronized monitors and blocking primitives with `java.util.concurrent.locks.ReentrantLock`, semaphore pools, and virtual-thread-safe non-blocking structures.
- **Memory Footprint & ThreadLocals:** Documents memory leak risks associated with deep `ThreadLocal` inheritance patterns in high-concurrency virtual thread pools and benchmarks migration to `ScopedValue`.

### 2. [aetherkv](https://github.com/mohameddhamed/aetherkv) (Rust)
*Ultra-high-throughput, asynchronous Log-Structured Merge (LSM) key-value storage engine engineered for modern NVMe solid-state drives.*
- **Lock-Free MemTable:** Implemented with a generational monotonic bump arena and lock-free SkipList, eliminating allocator mutex contention during high-ingest write bursts.
- **Pre-allocated WAL & Inode-Lock-Free Direct I/O:** Uses pre-allocated append-only log segments and Linux `io_uring` Direct I/O (`O_DIRECT`), bypassing OS page cache pollution and eliminating Linux file metadata serialization (`i_rwsem`).
- **4KB Delta SSTables & AVX2 Bloom Filters:** 4KB block-aligned sorted tables with prefix delta compression and vectorized AVX2 Block-Split Bloom filters achieving sub-microsecond point-lookup rejection.
- **Anti-Stall Compaction:** Leveled compaction pipeline featuring dynamic anti-stall backpressure to prevent catastrophic write pauses during Level-0 file accumulation.

### 3. [nexusloop](https://github.com/mohameddhamed/nexusloop) (C++20)
*Deterministic, zero-allocation quantitative trading runtime and zero-copy market data gateway.*
- **Cache-Conscious Lock-Free Rings:** SPSC and MPMC Disruptor ring buffers with 64-byte cache-line isolation, eliminating false sharing (MESI cache line bouncing) between producers and consumers.
- **Deterministic Memory & Zero-Allocation Trap:** Custom 2MB huge-page arena allocator paired with an allocation guard that intercepts heap allocation system calls on the hot path to enforce strict zero dynamic allocation guarantees.
- **SIMD Vectorized Ingestion:** AVX2/NEON vector shuffle parsing of NASDAQ TotalView-ITCH 5.0 messages, converting network big-endian wire formats into structured order book events in single-digit nanoseconds.
- **Dual I/O Engine:** Integrates Linux `io_uring` polling with fallback epoll and core affinitization for kernel-bypass-like deterministic low latency.

### 4. [mini-columnar-engine](https://github.com/mohameddhamed/mini-columnar-engine) (Rust)
*Lean, production-grade vectorized in-memory OLAP micro-database engine mirroring SAP HANA TableStore.*
- **Core Columnar Internals:** Contiguous memory vectors, bit-packed null masks (0.125 bytes/row), dictionary encoding with integer surrogate evaluation, and algebraic RLE aggregation.
- **Execution Engine:** Morsel-driven chunked execution (1024-row L1 cache resident batches), SIMD slice matching, and direct-indexed array accumulation for zero-hash-table grouping.
- **Performance:** **3.96 Billion elem/sec** contiguous scan throughput, **29.5x speedup** on GROUP BY, and 32 passing unit/integration tests with Criterion benchmarks.

### 5. [resp-storage-engine](https://github.com/mohameddhamed/resp-storage-engine) (Go)
*High-throughput concurrent in-memory key-value storage engine implementing the Redis Serialization Protocol (RESP2).*
- **Core Concurrency:** Zero-allocation byte builders, fine-grained `sync.RWMutex` read/write locking with zero data races verified under `go test -race`.
- **Transactions & Replication:** Connection-scoped isolated `MULTI`/`EXEC`/`DISCARD` transactions, master-replica replication with offset streaming, and binary RDB snapshot parsing.
- **Load Verification:** Built-in concurrent multi-threaded load generator demonstrating ~100k ops/sec with sub-millisecond P99 tail latency.

### 6. [while-x86-compiler](https://github.com/mohameddhamed/while-x86-compiler) (C++)
*Ahead-of-Time (AOT) compiler translating the While imperative language directly into 32-bit x86 NASM assembly and ELF binaries.*
- **Front-End & Analysis:** Flex scanner, Bisonc++ LALR(1) parser, abstract syntax tree (AST) generation, and static semantic symbol table validation.
- **Code Generation & Runtime Bridge:** 32-bit x86 register code generator (`eax`, `ebx`, `edx`, stack preservation) linked against a native C runtime (`io.c`) using the standard 32-bit `cdecl` calling convention.
- **Automated CI:** Comprehensive automated test suite and Ubuntu Linux CI pipeline verifying compilation, assembling, linking, and ELF execution.

### Additional Engineering Work: [parallel-crdt](https://github.com/mohameddhamed/parallel-crdt) (TypeScript)
*Real-time collaborative text editor extension for Visual Studio Code using Conflict-Free Replicated Data Types (CRDTs).*
- Built on Yjs binary state vectors and WebSocket transport, providing mathematically provable eventual consistency across distributed clients with selective undo via `Y.RelativePosition`.

---

## ⚡ Technical Competencies

- **Enterprise Java & Concurrency:** Java 21, Spring Boot, Project Loom (Virtual Threads), `java.util.concurrent`, Lock-Free Atomics, `ReentrantLock`, Carrier Starvation & Pinning Analysis, JVM Tuning, Garbage Collection (ZGC/G1), High-Throughput REST & Asynchronous Microservices
- **Systems & Database Internals:** Vectorized Execution (SIMD / AVX2), LSM-Tree Storage Engines, In-Memory OLAP Databases (SAP HANA TableStore), Lock-Free Ring Buffers (Disruptor), Memory Arena Allocators, Linux Direct I/O (`io_uring`, epoll)
- **Languages:** Java (Primary / Expert), Rust, Modern C++ (C++20), Go, SQL, TypeScript, 32-bit x86 Assembly
- **Distributed & Cloud Infrastructure:** Master-Replica Replication, Redis RESP2 Protocol, WebSockets & CRDTs, Docker, Linux Systems Programming, CI/CD (GitHub Actions), PostgreSQL
- **Benchmarking & Concurrency Verification:** ThreadSanitizer (TSan), AddressSanitizer (ASan), UBSan, Go `-race` detector, JMeter, Criterion.rs, NASM, Make
