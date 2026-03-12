# Colmap-HIP

[Original README](README.md.orig)

## Description

This is a modified version of colmap, added HIP in MVS (dense reconstruction) to support AMD GPUs.

## How to build

### 1. Install dependencies
```bash
sudo apt-get update
sudo apt-get install \
    git \
    cmake \
    ninja-build \
    build-essential \
    libboost-program-options-dev \
    libboost-graph-dev \
    libboost-system-dev \
    libeigen3-dev \
    libopenimageio-dev \
    openimageio-tools \
    libmetis-dev \
    libgoogle-glog-dev \
    libgtest-dev \
    libgmock-dev \
    libsqlite3-dev \
    libglew-dev \
    qt6-base-dev \
    libqt6opengl6-dev \
    libqt6openglwidgets6 \
    libcgal-dev \
    libceres-dev \
    libsuitesparse-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libmkl-full-dev  # optional
```
**You also need to install amdgpu driver and ROCm. Please refer to AMD's document for guide.**

### 2. Compile
```bash
git clone https://github.com/PowerfulGhost/colmap-hip
mkdir colmap-hip/build

# Configure
cd colmap-hip/build
export CMAKE_PREFIX_PATH=/opt/rocm  # Replace with your rocm installation directory
cmake .. -GNinja -DHIP_ENABLED=ON -DCUDA_ENABLED=OFF

# Compile and install
ninja
sudo ninja install  # Optional
```

## Usage
Basically the same as the original colmap.
Use `HIP_VISIBLE_DEVICES` environment variable to spicify which GPU(s) to use.

## Known Issues
SiftGPU is not supported by AMD gpus. Not sure why. Set use_gpu=0 to use SiftCPU instead (MVS still using GPU).

## If you find this project helpful, please consider giving it a star ⭐. Thank you!