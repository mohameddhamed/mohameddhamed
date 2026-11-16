# Mohamed Hamed

**Systems & Concurrency Engineer | Database Internals & Distributed Infrastructure**  
*M.Sc. Software Architecture @ Eötvös Loránd University (ELTE)*  
Budapest, Hungary • [LinkedIn](https://www.linkedin.com/in/mohameddhamed/) • [GitHub](https://github.com/mohameddhamed)

---

## 🛠️ Engineering Profile

I am a Systems and Concurrency Engineer with 3.5+ years of continuous enterprise backend experience in core database platforms and distributed runtime systems:
- **SAP (Core Platform):** Engineered internal storage and query execution layers for **SAP HANA TableStore**, focusing on in-memory columnar layouts, dictionary compression, vectorized filter pushdown, and direct-indexed grouping.
- **ExxonMobil (Distributed Systems):** Built high-throughput distributed logging infrastructure and enterprise service middleware.
- **Academic Research (M.Sc. Software Architecture):** Investigated Java 21 Project Loom virtual thread mechanics, carrier thread starvation, and synchronized block pinning in high-concurrency systems.

---

## 🏛️ The 5 Systems Pillars (Core Showcase)

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              THE 5 SYSTEMS PILLARS                                     │
├──────────────────────────────┬──────────────────────────────┬──────────────────────────┤
│ 1. mini-columnar-engine     │ 2. resp-storage-engine       │ 3. while-x86-compiler    │
│    (Rust)                    │    (Go)                      │    (C++)                 │
│    Vectorized In-Memory OLAP │    Concurrent In-Memory KV   │    AOT While-to-32bit    │
│    Engine (SAP HANA)         │    Store & RESP2 Protocol    │    x86 Assembly Compiler │
├──────────────────────────────┼──────────────────────────────┴──────────────────────────┤
│ 4. parallel-crdt             │ 5. virtual-thread-springs                               │
│    (TypeScript)              │    (Java 21)                                            │
│    Real-Time VS Code Buffer  │    M.Sc. Thesis Project Loom Virtual Thread Concurrency │
│    & Yjs CRDT Convergence    │    & Thread-Pinning Empirical Research                  │
└──────────────────────────────┴─────────────────────────────────────────────────────────┘
```

### 1. [mini-columnar-engine](https://github.com/mohameddhamed/mini-columnar-engine) (Rust)
*Lean, production-grade vectorized in-memory OLAP micro-database engine mirroring SAP HANA TableStore.*
- **Core Internals:** Contiguous memory vectors, bit-packed null masks (0.125 bytes/row), dictionary encoding with integer surrogate evaluation, and algebraic RLE aggregation.
- **Execution Engine:** Morsel-driven chunked execution (1024-row L1 cache resident batches), SIMD slice matching, and direct-indexed array accumulation for zero-hash-table grouping.
- **Performance:** **3.96 Billion elem/sec** contiguous scan throughput, **29.5x speedup** on GROUP BY, and 32 passing unit/integration tests with Criterion benchmarks.

### 2. [resp-storage-engine](https://github.com/mohameddhamed/resp-storage-engine) (Go)
*High-throughput concurrent in-memory key-value storage engine implementing the Redis Serialization Protocol (RESP2).*
- **Core Internals:** Zero-allocation byte builders, `sync.RWMutex` fine-grained read/write locking with zero data races verified under `go test -race`.
- **Transactions & Replication:** Connection-scoped isolated `MULTI`/`EXEC`/`DISCARD` transactions, master-replica replication with offset streaming, and binary RDB snapshot parsing.
- **Load Benchmark:** Includes concurrent multi-threaded load generator measuring ~100k ops/sec and sub-millisecond P99 latency.

### 3. [while-x86-compiler](https://github.com/mohameddhamed/while-x86-compiler) (C++)
*Ahead-of-Time (AOT) compiler translating the While imperative language directly into 32-bit x86 NASM assembly and ELF binaries.*
- **Core Internals:** Flex scanner, Bisonc++ LALR(1) parser, static semantic symbol table, and 32-bit x86 register code generator (`eax`, `ebx`, `edx`, stack preservation).
- **Runtime Bridge:** Links generated assembly with native C runtime (`io.c`) using the standard 32-bit `cdecl` calling convention.
- **CI / Testing:** Full automated test suite and Ubuntu Linux CI pipeline verifying compilation, assembling, linking, and program execution.

### 4. [parallel-crdt](https://github.com/mohameddhamed/parallel-crdt) (TypeScript)
*Real-time collaborative text editor extension for Visual Studio Code using Conflict-Free Replicated Data Types (CRDTs).*
- **Core Internals:** Built on Yjs binary state vectors and WebSocket transport, providing mathematically provable eventual consistency across distributed clients.
- **Selective Undo:** Resolves collaborative coordinate drift using `Y.RelativePosition` anchored to unique `(client, clock)` tuples rather than fragile absolute offsets.
- **Remote Presence:** Low-latency peer awareness protocol and custom VS Code cursor/selection highlight decorations.

### 5. [virtual-thread-springs](https://github.com/mohameddhamed/virtual-thread-springs) (Java 21)
*M.Sc. thesis research application and empirical benchmark study on Java 21 Project Loom.*
- **Core Internals:** Evaluates carrier thread starvation, synchronized block monitor pinning, and legacy ThreadLocal memory leaks under high-throughput MVC workloads.
- **Migration Architecture:** Documents safe concurrency refactoring strategies replacing synchronized monitors with `ReentrantLock` and non-blocking constructs.

---

## ⚡ Technical Competencies

- **Languages:** Rust, Go, C++, Java 21, TypeScript, SQL, 32-bit x86 Assembly
- **Systems & Internals:** Vectorized Execution (SIMD), In-Memory OLAP Engines, Memory Prefetching, CRDTs, Lock-Free Concurrency, Project Loom
- **Distributed & Cloud:** Master-Replica Replication, WebSockets, Docker, Linux, CI/CD (GitHub Actions), PostgreSQL
- **Benchmarking & Tooling:** Criterion.rs, Go `-race` detector, JMeter, NASM, Make
