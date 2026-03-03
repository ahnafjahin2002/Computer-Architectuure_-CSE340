# 🚁 Parallel Inference Engine for Autonomous Disaster Drones

## 📌 Project Overview

This project presents a **power-efficient parallel CNN inference engine** designed for **autonomous disaster response drones**.

The objective is to enable **real-time onboard survivor detection** in disaster environments where:

- ⚡ Power is strictly limited (< 2W)
- 🌐 Internet connectivity is unreliable or unavailable
- ⏱ Real-time inference is required (<150 ms per frame)

The system eliminates cloud dependency and performs **fully onboard AI inference** for faster and safer disaster response.

---

## 🎯 Project Objectives

- 🚀 Achieve real-time CNN inference (<150 ms latency)
- 🔋 Maintain total system power under 2W
- 🧠 Implement SPMD-based parallel processing
- 💾 Optimize memory hierarchy to reduce DRAM access
- 🛡 Ensure reliability in harsh environments

---

## 🏗 Proposed Architecture

### 🔹 Multi-Core SoC Design

- 4–8 RISC-based cores (RISC-V / ARM Cortex-A style)
- Shared L2 cache
- Private L1 cache per core
- SIMD vector processing support
- ECC-protected memory modules

Architecture principles are inspired by:
📘 Computer Organization and Design ARM Edition (Patterson & Hennessy, 2016)

---

## 🔄 Parallel Processing Model

### 🧩 SPMD (Single Program, Multiple Data)

- Each core runs the same CNN inference kernel
- Each core processes a different spatial partition of the input image
- Uniform workload distribution across cores

### ✅ Benefits

- ⚡ Higher throughput
- 📉 Reduced inference latency
- 🧠 Efficient multi-core utilization

---

## 🖼 Spatial Tiling Strategy

To efficiently process high-resolution images:

- Input frame divided into an **8×8 grid**
- Each tile processed independently
- Feature maps stored in L1 cache

### ✅ Advantages

- 📈 Improved data locality
- 📉 Lower cache miss rate
- ⚡ Faster convolution processing

---

## 💾 Memory Hierarchy Optimization

Embedded AI systems often suffer from the **memory wall problem**.

Optimization techniques implemented:

- 📦 CNN weights stored in Shared L2 cache (read-only)
- 🗂 Intermediate feature maps stored in private L1 caches
- 🔄 DMA-based direct camera-to-SRAM transfer
- 🚫 DRAM bypass to reduce off-chip traffic
- 📊 Cache miss rate maintained below 10%

### 🎯 Result

- 🔋 Power-efficient operation
- 🚀 Reduced memory latency
- ⚡ Faster inference

---

## 🧮 SIMD Acceleration

Each core uses:

- 🔢 SIMD vector instructions
- ⚙ Parallel Multiply-Accumulate (MAC) operations

This significantly accelerates convolution layers.

---

## 🛡 Reliability Features

To ensure robustness in disaster environments:

- 🧠 ECC (Error-Correcting Code) memory protection
- 🔄 Graceful degradation mechanism
  - Failed core workloads redistributed
  - System continues at reduced performance

---

## ⚙ Operating Modes

### 🚨 Rescue Mode (High Performance)

- All cores active
- High clock frequency
- Inference latency: <120 ms
- Power budget: 1.8W – 2.0W
- Use case: Active survivor detection

### 🌍 Survey Mode (Energy Saving)

- 2–3 cores active
- Reduced clock frequency
- Inference latency: ~400 ms
- Power budget: <1.0W
- Use case: Wide-area terrain mapping

---

## 📊 System Performance

- ⏱ Real-time inference latency: <150 ms
- 🔋 Average power consumption: ~1.8W
- 📉 Cache miss rate: <10%
- 🧠 Efficient weight sharing via Shared L2
- 🚀 Fully onboard processing (no cloud dependency)

---

## 🌍 Real-World Impact

This system:

- 🆘 Enables real-time survivor detection
- 🌐 Operates without cloud infrastructure
- 🛩 Increases drone autonomy
- 👨‍🚒 Reduces risk for human rescuers
- 🔋 Extends drone flight duration

It demonstrates practical application of **Computer Architecture concepts** to real-world humanitarian challenges.

---

## 📚 References

- Patterson, D. A., & Hennessy, J. L. (2016). Computer Organization and Design ARM Edition.
- NVIDIA Jetson Nano Technical Overview (2023).
- Zhou et al. (2024). AI Applications in UAV-Enabled Wireless Networks.

---

## 🏁 Conclusion

This project successfully designs a:

- 🔄 Parallel
- 🔋 Energy-efficient
- ⚡ Low-latency
- 🛡 Fault-tolerant

CNN inference engine for autonomous disaster drones.

By integrating SPMD parallelism, optimized memory hierarchy, SIMD acceleration, and fault tolerance mechanisms, the system achieves a balanced trade-off between performance, power efficiency, and reliability.
