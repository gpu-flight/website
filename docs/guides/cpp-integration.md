# C++ Integration Guide

This guide covers how to use `gpufl` in your CUDA C++ application.

## Basic Usage

To start capturing GPU telemetry, you need to include the `gpufl` header and initialize the library.

```cpp
#include <gpufl/gpufl.h>

int main() {
    // Initialize GPUFlight
    // This starts the background collector thread and CUPTI interception
    gfl::initialize();

    // ... your CUDA code ...

    // Shutdown GPUFlight to ensure all logs are flushed
    gfl::shutdown();
    return 0;
}
```

## Logical Scoping

One of the most powerful features of `gpufl` is the ability to group multiple kernel launches into "Logical Scopes". This helps you understand high-level application phases rather than just individual kernels.

Use the `GFL_SCOPE` macro (or `gfl::Scope` object) to define these regions.

```cpp
void run_inference() {
    GFL_SCOPE("InferencePhase");

    // All kernels launched within this block will be 
    // associated with "InferencePhase" in the logs.
    my_kernel_1<<<...>>>(...);
    my_kernel_2<<<...>>>(...);
}
```

## How it Works

1.  **CUPTI Interception**: `gpufl` uses the NVIDIA CUPTI callbacks to intercept every `cudaLaunchKernel` call.
2.  **Lock-Free Logging**: Metadata about the kernel (name, grid/block dims, etc.) is pushed into a lock-free ring buffer.
3.  **Background Collection**: A separate thread pulls data from the ring buffer and writes it to NDJSON logs. This minimizes the impact on the application's critical path.
