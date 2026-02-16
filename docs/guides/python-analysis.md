# Python Analysis & Visualization

The `gpufl` Python library provides a suite of tools for analyzing the structured logs (NDJSON) produced by the C++ library.

## Analyzer (CLI Dashboard)

The `analyzer` module provides an "Executive Summary" of GPU performance directly in your terminal.

```python
from gpufl.analyzer import GpuFlightSession

# Load a session (automatically picks up .kernel, .scope, and .system logs)
session = GpuFlightSession("./logs", log_prefix="stress")

# 1. Executive Summary: Duration, Utilization, Peak VRAM
session.print_summary()

# 2. Hierarchical Scope Analysis: Time spent in GFL_SCOPE blocks
session.inspect_scopes()

# 3. Kernel Hotspots: Top expensive kernels with Stack Trace visualization
session.inspect_hotspots(top_n=5, max_stack_depth=5)
```

## Visualization (Timeline)

The `viz` module creates interactive `matplotlib` plots to correlate kernel execution with system metrics.

```python
import gpufl.viz as viz

# Load all logs in a directory
viz.init("./logs/*.log")

# Show interactive timeline with:
# - GPU/Host utilization & VRAM
# - Kernel occupancy markers
# - Hover-able kernel names
viz.show()
```

### Key Visualization Features
- **GPU/Host utilization**: Correlate code execution with hardware load.
- **Kernel occupancy**: See how well your kernels are utilizing the GPU.
- **Interactive Tooltips**: Hover over kernels in the timeline to see their full name and metadata.
