# Testing

The GPUFlight project includes comprehensive test suites for both the C++ and Python components.

## C++ Tests (GoogleTest)

The C++ tests are hardware-aware and will automatically skip NVIDIA-specific tests if a compatible GPU or driver is not detected.

1.  **Build the tests**:
    ```bash
    cmake --build build --target gpufl_tests
    ```

2.  **Run via CTest**:
    ```bash
    ctest --test-dir build --output-on-failure
    ```

3.  **Run directly**:
    ```bash
    ./build/tests/gpufl_tests
    ```

## Python Tests (pytest)

The Python tests use `pytest` and verify the analyzer and visualization logic, often using mocked data to avoid hardware dependencies during CI.

1.  **Install pytest**:
    ```bash
    pip install pytest
    ```

2.  **Run tests**:
    ```bash
    # Ensure python directory is in PYTHONPATH
    export PYTHONPATH=$PYTHONPATH:$(pwd)/python
    pytest tests/python
    ```
