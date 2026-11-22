# Mohamed Hamed

**Application Developer at SAP | Java backend engineering & JVM concurrency research**
*M.Sc. in Computer Science (Software Architecture), in progress at Eötvös Loránd University (ELTE)*
Budapest, Hungary • [LinkedIn](https://www.linkedin.com/in/mohameddhamed/) • [GitHub](https://github.com/mohameddhamed)

[![Java 21](https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Rust](https://img.shields.io/badge/Rust-1.80%2B-DEA584?logo=rust&logoColor=black)](https://www.rust-lang.org/)
[![C++20](https://img.shields.io/badge/C%2B%2B-20-00599C?logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
[![Go](https://img.shields.io/badge/Go-1.22%2B-00ADD8?logo=go&logoColor=white)](https://go.dev/)

---

## 🛠️ Engineering Profile

I have been an Application Developer at SAP since September 2026. I fixed a duplicate-key defect in an application within the SAP HANA ecosystem by implementing a data migration and a uniqueness constraint. I also contributed NetBox DCIM integration and live power telemetry to data center observability tooling.

My earlier SAP roles were Software Developer and Backend Developer. I refactored ABAP business logic into SAP CAP and Spring Boot services and implemented REST/OData endpoints and automated API tests.

At ExxonMobil, I progressed from Automation Developer to Full Stack Developer to Backend Software Developer. I designed and implemented a Spring Boot workflow for AI-assisted document analysis, with background jobs and polling endpoints for status and results. My earlier work covered .NET, SQL Server and TypeScript configuration tooling.

My ELTE research examines virtual thread scheduling and contention in Spring Boot. My independent projects explore storage, networking and compilers.

---

## 🏛️ Flagship Showcase (Core Pillars)

| System / Repository | Primary Stack | Domain / Focus | Key Architectural Highlights | CI / Verification |
| :--- | :--- | :--- | :--- | :---: |
| **[virtual-thread-springs](https://github.com/mohameddhamed/virtual-thread-springs)** | Java, Spring Boot | JVM concurrency research | Carrier pinning, critical-section serialization, native blocking and pool contention | [Thesis PDF](https://github.com/mohameddhamed/virtual-thread-springs/blob/main/overleaf/main.pdf) |
| **[aetherkv](https://github.com/mohameddhamed/aetherkv)** | Rust | Experimental LSM storage | Arena-backed skiplist MemTable, WAL, SSTables and compaction. Known restart recovery defect. | [CI](https://github.com/mohameddhamed/aetherkv/actions/workflows/ci.yml) |
| **[nexusloop](https://github.com/mohameddhamed/nexusloop)** | C++20 | Market-data prototype | Padded SPSC ring, ITCH parser and in-memory benchmarks | [CI](https://github.com/mohameddhamed/nexusloop/actions/workflows/ci.yml) |
| **[mini-columnar-engine](https://github.com/mohameddhamed/mini-columnar-engine)** | Rust | Typed analytical operators | Bit-packed null masks, dictionary encoding and grouping over pre-encoded dense keys | [CI](https://github.com/mohameddhamed/mini-columnar-engine/actions/workflows/ci.yml) |
| **[resp-storage-engine](https://github.com/mohameddhamed/resp-storage-engine)** | Go, RESP2 | In-memory key-value store | Per-connection command queues, read/write locking and replication | [CI](https://github.com/mohameddhamed/resp-storage-engine/actions/workflows/ci.yml) |
| **[while-x86-compiler](https://github.com/mohameddhamed/while-x86-compiler)** | **C++**, x86 Assembly | Ahead-of-Time (AOT) Compiler | Flex/Bisonc++ LALR(1) front-end, AST semantic analysis, 32-bit x86 NASM code generator, standard C ABI bridge (`cdecl`) | [![CI](https://github.com/mohameddhamed/while-x86-compiler/actions/workflows/ci.yml/badge.svg)](https://github.com/mohameddhamed/while-x86-compiler/actions/workflows/ci.yml) |

---

## 🔬 Deep-Dive Project Breakdowns

### 1. [virtual-thread-springs](https://github.com/mohameddhamed/virtual-thread-springs) (Java 21, Spring Boot)
In the six October 15 Java 21 runs on an Apple M1, changing the lock from `synchronized` to `ReentrantLock` reduced JFR pin events from 108 to zero per run. At 10 virtual users, mean steady throughput was 1.967 and 1.956 req/s respectively. Both locks serialized the 500 ms operation. See the [results chapter](https://github.com/mohameddhamed/virtual-thread-springs/blob/main/overleaf/chapters/06-results.tex) for this comparison and the separate JDK and workload strata.

### 2. [aetherkv](https://github.com/mohameddhamed/aetherkv) (Rust)

Storage prototype with a skiplist MemTable and bump arena, an append-only WAL, block SSTables, Bloom filters and leveled compaction. A restart test lost an acknowledged key with sync-on-write enabled.

### 3. [nexusloop](https://github.com/mohameddhamed/nexusloop) (C++20)

An ITCH 5.0 parser and padded SPSC ring. The parser benchmark repeatedly decodes a warmed in-memory buffer and compares against a scalar baseline. The baseline can be faster. Handoff timing is from a separate ping-pong microbenchmark.

### 4. [mini-columnar-engine](https://github.com/mohameddhamed/mini-columnar-engine) (Rust)

Contiguous typed columns, validity bitmaps, selection vectors and direct-indexed grouping. Archived Criterion timings cover scan plus sum and grouping on one million pre-encoded rows. Grouping can omit null keys and all-null groups.

### 5. [resp-storage-engine](https://github.com/mohameddhamed/resp-storage-engine) (Go)

RESP2 command handling, per-connection `MULTI`/`EXEC` queues and replication. Other clients' operations can interleave with the execution of queued commands. No races were detected in the audited race-enabled test run.

### 6. [while-x86-compiler](https://github.com/mohameddhamed/while-x86-compiler) (C++)
*Ahead-of-Time (AOT) compiler translating the While imperative language directly into 32-bit x86 NASM assembly and ELF binaries.*
- **Front-End & Analysis:** Flex scanner, Bisonc++ LALR(1) parser, abstract syntax tree (AST) generation, and static semantic symbol table validation.
- **Code Generation & Runtime Bridge:** 32-bit x86 register code generator (`eax`, `ebx`, `edx`, stack preservation) linked against a native C runtime (`io.c`) using the standard 32-bit `cdecl` calling convention.
- **Automated CI:** Comprehensive automated test suite and Ubuntu Linux CI pipeline verifying compilation, assembling, linking, and ELF execution.

### Additional Engineering Work: [parallel-crdt](https://github.com/mohameddhamed/parallel-crdt) (TypeScript)
*Real-time collaborative text editor extension for Visual Studio Code using Conflict-Free Replicated Data Types (CRDTs).*
- Integrated Yjs document synchronization over a WebSocket server.

---

## ⚡ Technical Competencies

- **Java backend and JVM research:** Spring Boot, SAP CAP, REST/OData, JFR and virtual-thread experiments
- **Independent systems work:** columnar analytics, LSM storage prototypes, SPSC rings and RESP2
- **Languages:** Java, Rust, C++20, Go, SQL and TypeScript
- **Distributed & Cloud Infrastructure:** Master-Replica Replication, Redis RESP2 Protocol, WebSockets & CRDTs, Docker, Linux Systems Programming, CI/CD (GitHub Actions), PostgreSQL
- **Benchmarking & Concurrency Verification:** ThreadSanitizer (TSan), AddressSanitizer (ASan), UBSan, Go `-race` detector, JMeter, Criterion.rs, NASM, Make
