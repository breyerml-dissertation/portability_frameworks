# SYCL

An DAXPY example using the SYCL programming framework.
The two SYCL implementations DPCPP/icpx and AdaptiveCpp are supported.

## icpx

To use DPCPP/icpx as SYCL compiler, specify `-DEXAMPLE_SYCL_IMPLEMENTATION="icpx"`.

```bash
cmake -DCMAKE_CXX_COMPILER=icpx -DEXAMPLE_SYCL_IMPLEMENTATION="icpx" -DEXAMPLE_SYCL_OFFLOAD_DEVICE_TYPE="gpu" -B build .
cmake --build build
build/sycl_daxpy
```

The target device, `cpu` or `gpu`, can be switched using the `EXAMPLE_SYCL_OFFLOAD_DEVICE_TYPE` option.
Note that the respective `-fsycl-targets` flag depends on the targeted GPU and must be separately set via
`CMAKE_CXX_FLAGS`.

The target flags are:

- CPUs: `-fsycl -fsycl-targets=spir64_x86_64`
- NVIDIA GPUs: `-fsycl -fsycl-targets=nvidia_gpu_sm_80`
- AMD GPUs: `-fsycl -fsycl-targets=amd_gpu_gfx90a`
- Intel GPUs: `-fsycl -fsycl-targets=intel_gpu_bmg_g21"`

Note that the offload architectures have to be replaced with the respective architecture of the target device. 

## AdaptiveCpp

To use AdaptiveCpp as SYCL compiler, specify `-DEXAMPLE_SYCL_IMPLEMENTATION="acpp"`.

```bash
cmake -DEXAMPLE_SYCL_IMPLEMENTATION="acpp" -DEXAMPLE_SYCL_OFFLOAD_DEVICE_TYPE="gpu" -B build .
cmake --build build
build/sycl_daxpy
```

The target device, `cpu` or `gpu`, can be switched using the `EXAMPLE_SYCL_OFFLOAD_DEVICE_TYPE` option.
The AdaptiveCpp target can be changed via the `ACPP_TARGETS` environment variable (default: `generic`).