# GPU Benchmarking on Mandrake Server

This document provides a comprehensive guide to the benchmarking process performed on the **Mandrake** server at **IIT Delhi**, including details of the installed software, commands executed, and the results obtained.

## 1. System Overview

### 1.1 Server Details
- **Server Name**: Mandrake
- **Location**: IIT Delhi
- **GPU**: Tesla T4
- **CUDA Version**: 12.1
- **NVIDIA Driver Version**: 12.1
- **CUDA Runtime Version**: 11.3

## 2. Installed Tools and Versions

### 2.1 CUDA Toolkit and Samples
- **CUDA Toolkit Version**: 12.1 (Includes `nvcc`, `deviceQuery`, `bandwidthTest`, `matrixMul`, etc.)
- **CUDA Samples Location**: `/usr/local/cuda/samples/`

The **CUDA Samples** directory contains several benchmarking tools that were used to evaluate the GPU performance, including:
- `deviceQuery`
- `bandwidthTest`
- `matrixMul`

### 2.2 NVIDIA SMI (System Management Interface)
- **Version**: 530.41.03

NVIDIA SMI is used for real-time monitoring of GPU stats, including memory usage, GPU utilization, temperature, and more.

## 3. Benchmarking Steps

### 3.1 Step 1: Checking GPU Details Using `deviceQuery`
We started by compiling and running the `deviceQuery` sample, which provides information about the GPU.

#### Command:
```bash
cd /usr/local/cuda/samples/1_Utilities/deviceQuery
sudo make
./deviceQuery
```
#### Output:
```
./deviceQuery Starting...

CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "Tesla T4"
  CUDA Driver Version / Runtime Version          12.1 / 11.3
  CUDA Capability Major/Minor version number:    7.5
  Total amount of global memory:                 14966 MBytes (15693381632 bytes)
  (040) Multiprocessors, (064) CUDA Cores/MP:    2560 CUDA Cores
  GPU Max Clock rate:                            1590 MHz (1.59 GHz)
  Memory Clock rate:                             5001 MHz
  Memory Bus Width:                              256-bit
  L2 Cache Size:                                 4194304 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
  Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total shared memory per multiprocessor:        65536 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  1024
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 3 copy engine(s)
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Enabled
  Device supports Unified Addressing (UVA):      Yes
  Device supports Managed Memory:                Yes
  Device supports Compute Preemption:            Yes
  Supports Cooperative Kernel Launch:            Yes
  Supports MultiDevice Co-op Kernel Launch:      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 175 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 12.1, CUDA Runtime Version = 11.3, NumDevs = 1
Result = PASS
```
### 3.2 Step 2: Measuring Bandwidth with bandwidthTest
Next, we ran the bandwidthTest sample to measure the GPU's memory bandwidth in different directions (Host to Device, Device to Host, Device to Device).

#### Command:
```bash
cd /usr/local/cuda/samples/1_Utilities/bandwidthTest
sudo make
./bandwidthTest
```
#### Output:
```
[CUDA Bandwidth Test] - Starting...
Running on...

Device 0: Tesla T4
Quick Mode

Host to Device Bandwidth, 1 Device(s)
PINNED Memory Transfers
  Transfer Size (Bytes)        Bandwidth(GB/s)
  32000000                     6.1

Device to Host Bandwidth, 1 Device(s)
PINNED Memory Transfers
  Transfer Size (Bytes)        Bandwidth(GB/s)
  32000000                     6.6

Device to Device Bandwidth, 1 Device(s)
PINNED Memory Transfers
  Transfer Size (Bytes)        Bandwidth(GB/s)
  32000000                     239.6

Result = PASS
```

### 3.3 Step 3: Evaluating Matrix Multiplication with matrixMul
The matrixMul sample was executed to test the GPU's computational performance using matrix multiplication.

#### Command:
```bash
cd /usr/local/cuda/samples/0_Simple/matrixMul
sudo make
./matrixMul
```

#### Output:
```
[Matrix Multiply Using CUDA] - Starting...
GPU Device 0: "Turing" with compute capability 7.5

MatrixA(320,320), MatrixB(640,320)
Computing result using CUDA Kernel...
done
Performance= 408.85 GFlop/s, Time= 0.321 msec, Size= 131072000 Ops, WorkgroupSize= 1024 threads/block
Checking computed result for correctness: Result = PASS
```

## 4. Summary of Results

### 4.1 `deviceQuery` Output
- **GPU Detected**: Tesla T4
- **CUDA Compute Capability**: 7.5
- **Total Global Memory**: 14966 MB
- **CUDA Cores**: 2560
- **Max GPU Clock Speed**: 1590 MHz

### 4.2 `bandwidthTest` Output
- **Host to Device Bandwidth**: 6.1 GB/s
- **Device to Host Bandwidth**: 6.6 GB/s
- **Device to Device Bandwidth**: 239.6 GB/s

### 4.3 `matrixMul` Output
- **Performance**: 408.85 GFLOPS
- **Time**: 0.321 ms
- **Operations**: 131,072,000 Ops
- **Workgroup Size**: 1024 threads/block

## 5. Conclusion

The benchmarking tests on the Mandrake server using CUDA samples have provided useful insights into the capabilities of the Tesla T4 GPU. The tests included:

- **Device details**: Verified GPU specifications using `deviceQuery`.
- **Memory bandwidth**: Measured transfer speeds between host and device, as well as device-to-device bandwidth, with impressive results for the Tesla T4.
- **Compute performance**: Evaluated GPU computational power using matrix multiplication, achieving a performance of 408.85 GFLOPS.

These results indicate that the GPU is capable of handling high-throughput data transfers and computation-intensive tasks efficiently.
