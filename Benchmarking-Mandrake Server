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
- **Version**: Installed with the NVIDIA driver.

NVIDIA SMI is used for real-time monitoring of GPU stats, including memory usage, GPU utilization, temperature, and more.

## 3. Benchmarking Steps

### 3.1 Step 1: Checking GPU Details Using `deviceQuery`
We started by compiling and running the `deviceQuery` sample, which provides information about the GPU.

#### Commands:
```bash
cd /usr/local/cuda/samples/1_Utilities/deviceQuery
sudo make
./deviceQuery
```
