# Chapter 1: Reliable, Scalable, and Maintainable Applications

**Source:** Designing Data-Intensive Applications, Chapter 1

## Introduction
[cite_start]Data-intensive applications are those where the limiting factor is the amount, complexity, or changing speed of data, rather than CPU power[cite: 35]. These applications are typically built from standard building blocks:
* [cite_start]**Databases:** Store data for later retrieval[cite: 38].
* [cite_start]**Caches:** Remember expensive operation results to speed up reads[cite: 39].
* [cite_start]**Search Indexes:** Allow filtering and keyword searching[cite: 40].
* [cite_start]**Stream Processing:** Handle asynchronous message sending[cite: 41].
* [cite_start]**Batch Processing:** Periodically crunch accumulated data[cite: 42].

[cite_start]Modern systems often combine these tools because single tools rarely meet all requirements[cite: 63]. [cite_start]When combining tools, the application developer essentially becomes a data system designer[cite: 93].

---

## 1. Reliability
[cite_start]Reliability essentially means "continuing to work correctly, even when things go wrong"[cite: 120].

### Faults vs. Failures
* [cite_start]**Fault:** A component of the system deviating from its spec[cite: 127].
* [cite_start]**Failure:** The system as a whole stops providing the required service to the user[cite: 127].
* [cite_start]**Goal:** Design fault-tolerant mechanisms that prevent faults from causing failures[cite: 129].

### Types of Faults
1.  **Hardware Faults:**
    * [cite_start]Examples include hard disk crashes, RAM faults, and power blackouts[cite: 140].
    * [cite_start]Hard disks have a mean time to failure (MTTF) of 10–50 years[cite: 142].
    * [cite_start]**Solution:** Redundancy (RAID, dual power supplies) is the standard approach to keep machines running[cite: 144, 145].

2.  **Software Errors:**
    * [cite_start]These are systematic errors that are harder to anticipate and correlated across nodes[cite: 159, 160].
    * [cite_start]Examples include software bugs (e.g., the Linux leap second bug), runaway processes, or cascading failures[cite: 162, 163, 168].
    * [cite_start]**Solution:** Process isolation, allowing processes to crash/restart, and thorough monitoring[cite: 172, 173].

3.  **Human Errors:**
    * [cite_start]Configuration errors are a leading cause of outages[cite: 178].
    * **Solutions:**
        * [cite_start]Design abstractions that discourage "the wrong thing"[cite: 181].
        * [cite_start]Provide sandbox environments for experimentation[cite: 184].
        * [cite_start]Implement quick recovery tools (rollbacks)[cite: 188].
        * [cite_start]Detailed telemetry and monitoring[cite: 191].

---

## 2. Scalability
[cite_start]Scalability is a system's ability to cope with increased load[cite: 206]. [cite_start]It is not a binary label; we must discuss how to cope with specific growth parameters[cite: 210].

### Describing Load
[cite_start]Load is described by **load parameters**, such as requests per second, read/write ratios, or hit rates[cite: 215, 216].

**Case Study: Twitter**
[cite_start]Twitter has two primary operations: Posting tweets (4.6k/sec average) and viewing Home Timelines (300k/sec)[cite: 221, 223]. [cite_start]The challenge is the "fan-out" (each user follows many people)[cite: 225].
* **Approach 1 (Pull):** Insert tweets into a global table. When a user reads their timeline, look up everyone they follow and merge tweets. [cite_start]This struggled with read load[cite: 227, 270].
* **Approach 2 (Push):** Maintain a cached timeline for each user. When a tweet is posted, insert it into the caches of all followers. [cite_start]This struggled with write load for celebrities (users with millions of followers)[cite: 236, 275].
* [cite_start]**Hybrid Approach:** Twitter now uses a hybrid approach where celebrity tweets are fetched separately (Approach 1) while normal tweets are pushed to caches (Approach 2)[cite: 280, 281].

### Describing Performance
* [cite_start]**Throughput:** Used for batch systems (records processed per second)[cite: 289].
* [cite_start]**Response Time:** Used for online systems (time between request and response)[cite: 290].
* [cite_start]**Latency vs. Response Time:** Latency is the time waiting to be handled; response time includes processing[cite: 297, 298].

**Percentiles:**
* Averages (means) mask issues; [cite_start]**percentiles** (p50, p95, p99) are better metrics[cite: 314, 315].
* [cite_start]**Median (p50):** Good for understanding the "typical" user experience[cite: 318].
* [cite_start]**Tail Latency (p95, p99):** Important because slow requests often affect the most valuable customers (those with the most data)[cite: 325, 327].
* [cite_start]**Head-of-line blocking:** One slow request can delay subsequent requests, making client-side measurement crucial[cite: 337, 339].

### Approaches for Coping with Load
* [cite_start]**Scaling Up (Vertical):** Moving to more powerful machines[cite: 383].
* [cite_start]**Scaling Out (Horizontal):** Distributing load across multiple smaller machines (shared-nothing architecture)[cite: 383, 384].
* [cite_start]**Elasticity:** Automatically adding resources when load increases[cite: 387].
* [cite_start]There is no "magic scaling sauce"; architectures must be specific to the application's read/write volume and data complexity[cite: 395].

---

## 3. Maintainability
[cite_start]The majority of software cost lies in ongoing maintenance, not initial development[cite: 404].

### Three Design Principles
1.  **Operability (Making life easy for operations):**
    * [cite_start]Good operations can work around bad software, but not vice versa[cite: 421].
    * [cite_start]Systems should provide visibility (monitoring), good documentation, and predictable behavior[cite: 438, 441, 444].

2.  **Simplicity (Managing complexity):**
    * [cite_start]As projects grow, they risk becoming a "big ball of mud"[cite: 448].
    * [cite_start]**Accidental Complexity:** Complexity not inherent in the problem but arising from implementation[cite: 456].
    * [cite_start]**Abstraction:** The best tool to remove accidental complexity (hiding details behind a clean façade)[cite: 457, 458].

3.  **Evolvability (Making change easy):**
    * [cite_start]Requirements are always in flux[cite: 469].
    * [cite_start]Closely linked to simplicity; simple systems are easier to modify[cite: 477].
    * [cite_start]Agile patterns and refactoring help adapt to change at the system level[cite: 473, 476].