Description of the Work Done in This Project

In this project, I designed and analyzed a parallel CNN inference architecture tailored for autonomous disaster response drones operating under strict power and latency constraints. The main objective was to achieve real-time onboard image inference (under 150 ms latency) within a limited power budget of less than 2W.

To accomplish this, I proposed a multi-core System-on-Chip (SoC) architecture consisting of 4–8 RISC-based cores (such as RISC-V or ARM Cortex-A) using the SPMD (Single Program, Multiple Data) parallel execution model. Inspired by concepts discussed in Computer Organization and Design ARM Edition, I applied data-parallel workload distribution where each core executes the same CNN inference kernel but processes different spatial partitions of the input image.

I implemented a spatial tiling strategy, dividing high-resolution input frames into an 8×8 grid. Each core processes one tile independently, improving parallel throughput and reducing inference latency. Additionally, SIMD vectorization was incorporated at the core level to accelerate multiply-accumulate (लेट) operations used in convolution layers.

A major contribution of this project is the memory hierarchy optimization to overcome the “memory wall” problem observed in embedded AI platforms such as NVIDIABand Jetson Nano. To reduce costly DRAM access:

CNN weights are stored in a shared L2 cache for efficient read-only access.

Intermediate feature maps are stored in private L1 caches.

Tile sizes are adjusted according to L1 capacity to minimize cache misses.

DMA-based direct camera-to-SRAM routing is used to bypass DRAM and reduce off-chip memory traffic.

This architecture maintains cache miss rates below 10% and significantly lowers power consumption.

To improve reliability in harsh disaster environments, I integrated:

ECC (Error-Correcting Code) protection for memory modules

A graceful degradation mechanism where workloads are dynamically reallocated if a core fails

Furthermore, I proposed two operational modes:

Rescue Mode (high performance, <120 ms latency, ~1.8W power)

Survey Mode (energy-saving, ~400 ms latency, <1W power)

This dual-mode design allows adaptive performance scaling depending on mission requirements.

Overall, this project demonstrates how core Computer Architecture principles — parallelism, memory hierarchy optimization, SIMD acceleration, and fault tolerance — can be applied to build an energy-efficient real-time AI inference engine for autonomous disaster response drones.
