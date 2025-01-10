# Enabling NVIDIA Driver, NVIDIA SMI, and GPU Access on Mandrake Server

This document provides details of the steps taken to enable NVIDIA drivers, NVIDIA System Management Interface (SMI), and GPU access on the **Mandrake** server at **IIT Delhi**. Initially, GPU resources were inaccessible due to missing drivers and necessary configurations.

## System Specifications

- **Server Name:** Mandrake
- **GPU Model:** Tesla T4
- **NVIDIA Driver Version:** 530.41.03
- **CUDA Version:** 12.1 (via NVIDIA SMI), 11.3 (via nvcc)
- **GCC Version:** 7.5.0
- **GLIBC Version:** 2.27
- **Linux Kernel Version:** 4.15.0-213-generic
- **CUDA Toolkit Installed Version:** 11.3.1
- **Python Version:** 3.6.9

## Installation Steps

1. **NVIDIA Driver Installation**
   - **Issue:** The `nvidia-smi` command was non-functional due to missing NVIDIA drivers.
   - **Resolution Steps:**
      - Install the NVIDIA driver using:
       ```bash
       sudo apt-get install nvidia-driver-530
       ```
       
2. **Verification of NVIDIA Driver Installation**
   - Verify the driver installation using:
     ```bash
     nvidia-smi
     ```

3. **CUDA Toolkit Installation**
   - **Issue:** Post NVIDIA driver installation, CUDA compiler `nvcc` was missing.
   - **Resolution Steps:**
     - Install the CUDA toolkit using:
       ```bash
       sudo apt-get install nvidia-cuda-toolkit
       ```
     - Configure environment variables by adding the following to `~/.bashrc`:
       ```bash
       export PATH=/usr/local/cuda/bin:$PATH
       export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
       ```
     - Reload the bash profile:
       ```bash
       source ~/.bashrc
       ```

4. **Testing CUDA Installation**
   - The following CUDA script tests the GPU setup by printing "Hello testing GPU" from multiple threads on the GPU. It launches a kernel with one block containing ten threads.

      ```cpp
      #include <iostream>
      #include <cuda_runtime.h>
      
      __global__ void testKernel()
      {
          printf("Hello testing GPU\n");
      }
      
      int main()
      {
          testKernel<<<1,10>>>();
          cudaDeviceSynchronize();
          return 0;
      }
      ```

## Compatibility Matrix

| Component     | Installed Version | Compatible Versions/Requirements    |
|---------------|-------------------|------------------------------------|
| **CUDA Toolkit**  | 11.3.1            | Requires NVIDIA Driver 465.19.01 or newer |
| **NVIDIA Driver** | 530.41.03         | Compatible with CUDA 11.3.1 and 12.1      |
| **GLIBC**         | 2.27              | Minimum 2.17 required for CUDA 11.3.1     |
| **GCC**           | 7.5.0             | Compatible with CUDA 11.3.1 (recommended 8.x or newer) |

### Notes:
- **CUDA Toolkit Version 11.3.1** is compatible with **NVIDIA Driver** version **465.19.01** or newer. Current driver version **530.41.03** exceeds this requirement, supporting CUDA versions up to 12.1.
- **GLIBC 2.27** and **GCC 7.5.0** meet the minimum requirements for CUDA 11.3.1, though upgrading **GCC** to version **8.x** or newer is recommended for better support and performance.
- CUDA Toolkit release notes: [Link](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html)


## Reboot Requirements

1. **Post NVIDIA Driver Installation:**
   - A reboot was required to load the NVIDIA kernel module and enable the `nvidia-smi` command.

2. **Post CUDA Toolkit Installation:**
   - A reboot was recommended to ensure proper loading of CUDA-related environment variables and libraries.

## Verification Commands

- **Check NVIDIA Driver and GPU Status:**
  ```bash
  nvidia-smi
  ```
- **Check CUDA Compiler Version:**
  ```bash
  nvcc --version
  ```
- **Check GCC Version:**
  ```bash
  gcc --version
  ```
- **Check GLIBC Version:**
  ```bash
  ldd --version
  ```

## Troubleshooting
These were some of the issues and problems that one might face during the GPU Setup.

- **NVIDIA Driver Installation Issues:**
  - Ensure the correct version of the driver is installed matching the GPU model.
  - Check for any conflicts with existing kernel modules.

- **CUDA Toolkit Path Configuration:**
  - Ensure `PATH` and `LD_LIBRARY_PATH` environment variables are correctly set.
  - Verify by running a simple CUDA application.
