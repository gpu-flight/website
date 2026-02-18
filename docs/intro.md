---
sidebar_position: 1
---

# Introduction to GPUFlight

**GPUFlight (gpufl)** is a lightweight, always-on **GPU CUDA profiler and monitoring system** that records CUDA kernel behavior with minimal overhead, enabling post-mortem performance analysis and source-level correlation.

Unlike traditional GPU profilers (like NVIDIA Nsight) that often require stopping or significantly slowing down the application, GPUFlight is designed for **production GPU monitoring** with minimal overhead. It captures kernel telemetry and logical scopes into structured logs, providing deep insights into GPU workloads as they happen.

## 🚀 Key Features of GPUFlight CUDA Profiler

- **Real-time GPU Monitoring**: Automatically intercepts all CUDA kernel launches via CUPTI.
- **Production-Ready CUDA Profiler**: Uses a **Lock-Free Ring Buffer** and a **Background Collector Thread** to decouple logging from your hot path.
- **Logical Scoping**: Group thousands of micro-kernels into meaningful phases (e.g., "Inference", "PhysicsStep") using `GFL_SCOPE`.
- **Rich Metadata**: Captures Kernel Names, Grid/Block dimensions, Register counts, and Shared Memory usage.
- **Sidecar Ready**: Outputs structured NDJSON logs designed to be tailed by a separate Agent/Crawler (e.g., Kafka/Elastic).
- **Vendor Agnostic Design**: Architecture ready for AMD (ROCm) support.
