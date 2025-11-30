# **Containers Learning Roadmap**

*A structured, iterative journey into containers, Linux internals, and container runtime fundamentals*

---

## **📌 Purpose of This Curriculum**

This curriculum is designed to take you from *practical user of containers* to someone who can **accurately reason about**, **diagnose**, **optimize**, and eventually **rebuild key components of** the container ecosystem.

It emphasizes:

* Strong **hands-on building**
* Iterative **theory → practice → deeper theory**
* Linux-first understanding (Ubuntu VM)
* Multi-language exposure (Python, TS/Node.js, Go, Java)
* Clean code, clean structure
* Building real projects per milestone
* Eventually writing a **mini container runtime**
  (to demystify Docker forever)

This repo acts as a monorepo for:

* Curriculum & explanations
* Exercises & demos
* Real, functioning projects
* Your future personal “container toolkit”

---

# **🏗 Learning Philosophy**

1. **Iterative depth**

   * Start with low/medium theory & simple demos
   * Advance to medium theory & strong practicals
   * Optional deeper runtime internals (when appropriate)

2. **Linux-first**
   All deep learning is done in an **Ubuntu VM**, not Docker Desktop.
   A strong Linux foundation is essential.

3. **Code-first**
   Every concept has code, exercises, and mini-projects.

4. **Language-agnostic mastery**
   You will build containers in:

   * Python
   * TypeScript (Node.js)
   * Go
   * Java
     and learn how to optimize each.

5. **Runtime understanding without getting lost**
   You’ll understand containerd, runc, the OCI spec, namespace syscalls, cgroups v2, overlayfs — but in *practical layers*, not cold theory.

6. **Production-aligned habits**
   Even though early stages avoid cloud, later milestones prepare you to:

   * deploy real services
   * integrate CI
   * write secure, optimized Dockerfiles
   * understand container behavior under load

---

# **🧭 High-Level Roadmap Overview**

This curriculum is divided into **milestones**.
Each milestone contains:

* Concept notes
* Interactive demos
* Challenges/exercises
* A milestone project
* Optional “deep dive” material
* Documentation + reflection prompts

---

# **📚 Milestones Overview**

Below is the *canonical* progression of your learning path.

---

## **Milestone 0 — Environment Setup & Foundations**

**Goal:** Build your Ubuntu VM and prepare local tooling.

You will:

* Install Ubuntu VM
* Install Docker Engine
* Learn basics of Linux directory structure
* Learn package management, systemd, basic networking tools
* Git + VSCode + (Neo)Vim setup
* Install Go, Python, Node.js, Java SDKs

**Output:** A working development environment + notes in `curriculum/00_overview.md`

---

## **Milestone 1 — Single-Container Fundamentals**

**Goal:** Understand what a container *actually is*.

Topics:

* What is a process?
* What is a root filesystem?
* What is a Docker image?
* RUN vs CMD vs ENTRYPOINT
* Layers, caching, build context
* Ports, networking basics
* PID1 & signal forwarding
* Container logs → stdout/stderr

**Projects:**

* Build the same app in 4 languages
* Create minimal images (Alpine → Debian → scratch)
* Explore image layering using `docker history`

**Output folder:** `milestones/01_single_container_basics/`

---

## **Milestone 2 — Multi-Container Networking**

**Goal:** Combine containers into systems.

Topics:

* Docker networks
* Bridge networks & veth pairs
* DNS inside Docker networks
* Linking services
* Health checks
* Container-to-container communication
* Basic service discovery

**Project:**

* A 3-service system (API → worker → DB/cache)
* All written by you in Python/TS/Go/Java split
* Clean Dockerfiles
* Proper networking & health checks

`milestones/02_multi_container_networking/`

---

## **Milestone 3 — Images, Layers & Build Internals**

**Goal:** Master container image engineering.

Topics:

* Docker vs containerd vs runc
* OCI image spec overview
* Manifests, configs, layers
* Overlayfs internals
* Multi-stage builds
* Reproducible builds
* SBOMs
* Image size reduction techniques

**Project:**

* Optimize each language’s container image
* Produce a < 10MB Go image
* Produce a < 100MB Java image
* Multi-stage builds for Python & TS

---

## **Milestone 4 — Linux Internals for Containers**

**Goal:** Understand the primitives containers rely on.

Topics:

* Namespaces (PID, net, mount, uts, user, IPC)
* `unshare`, `clone`, `setns`
* `/proc/<pid>/ns` inspection
* Cgroups v2 basics
* `memory.max`, `cpu.max`, IO throttling
* Signals, process tree

**Interactive demos:**

* Create a manual network namespace
* Create a manual chroot environment
* Limit a process’s CPU & memory
* Explore namespaces used by Docker containers

**Project:**

* A “container simulator” — run processes in custom namespaces
  (next step toward mini-runtime)

---

## **Milestone 5 — Container Security**

**Goal:** Build intuition for container isolation & weaknesses.

Topics:

* Seccomp
* AppArmor
* Capabilities
* Rootless containers
* UID/GID mappings
* Image security / scanning
* Common container escape paths
* Supply chain considerations

**Project:**

* Build a hardened container
* Remove unnecessary capabilities
* Apply seccomp profile
* Run rootless variant
* Harden your multi-service project

---

## **Milestone 6 — Container Performance & Resource Engineering**

**Goal:** Learn how to diagnose and optimize container behavior.

Topics:

* CPU quotas vs shares
* Memory + OOM
* IO throttling
* Network bottlenecks
* cgroup metrics
* Container logs & filesystem pressure
* Performance tuning Dockerfiles

**Project:**

* Performance benchmark suite
* Compare performance between languages
* Stress-test containers with limits
* Document observations & optimizations

---

## **Milestone 7 — Kubernetes Integration (Local Only)**

**Goal:** Understand how Kubernetes actually uses container runtimes.

Topics:

* Pod sandbox
* Pause container
* Containerd’s CRI
* Pod networking
* Kubelet → containerd workflow
* Volumes & shared namespaces
* Pod lifecycle events

**Project:**

* Deploy earlier microservice project on Minikube/Kind
* Inspect runtime state under `/var/lib/containerd`
* Inspect pod namespace layouts

---

## **Milestone 8 — Runtime Internals**

**Goal:** Prepare to build a mini container runtime.

Topics:

* runc internals overview
* OCI runtime spec
* Lifecycle (create, start, delete)
* Rootfs unpacking
* Namespace setup sequence
* Cgroup creation sequence
* Pivot root
* Process execution in new namespaces

**Project:**

* Write code to manually:

  * create namespaces
  * configure cgroups
  * prepare a rootfs
  * run `/bin/sh` inside
* Start assembling pieces for your mini-runtime

---

## **Milestone 9 — Build a Mini Container Runtime**

**Goal:** Build a working, minimal container runtime in Go.

Your mini-runtime will:

* Create mount, PID, network, UTS namespaces
* Create cgroups for CPU/memory
* Setup rootfs
* Use `pivot_root`
* Exec a process inside the isolated environment
* Provide simple CLI (e.g., `mini-run --rootfs ./rootfs /bin/sh`)

**Stretch goals:**

* Basic networking (veth + bridge)
* Simple image unpacking
* Support basic OCI config.json fields

This is the capstone project.

`projects/04_mini_container_runtime/`

---

## **Milestone 10 — Real-World Container System (Optional)**

**Goal:** Deploy something real, applying everything learned.

Possible directions:

* Deploy microservices to EKS
* Build an AI/ML batch training pipeline
* Build an event-driven local system with production-like CI
* Implement hardened images
* Add logging/monitoring
* Add auto-scaling (KEDA, HPA)

This is optional and can be done anytime after milestone 6.

---

# **📂 Repo Structure**

A reminder of your repo’s canonical structure:

```
containers-learning/
  index.md                
  README.md              

  curriculum/
  milestones/
  projects/
  tools/
  .github/
```

This roadmap is anchored to that structure.

---

# **🧪 Multi-Language Commitment**

For each practical milestone, you will work with:

* Python
* TS/Node.js
* Go
* Java

You will learn how containers handle:

* dynamic runtimes (Python/Node)
* compiled static binaries (Go)
* heavyweight runtimes (Java)

This builds strong cross-language intuition.

---

# **🛠 Tooling Overview**

You will primarily use:

* **Ubuntu VM** for deep learning
* **Docker CE** (inside VM)
* **Docker Desktop or Colima** (on macOS) for convenience
* **Minikube / Kind** for Kubernetes
* **Go + Python** for tests & helper tools
* **VSCode + NeoVim** as editors
* **Markdown + Mermaid** for documentation

---

# **🧩 Your Workflow**

Every milestone contains:

* Notes
* Demos
* Exercises
* A project
* A self-written summary
* Optional deep dive section
