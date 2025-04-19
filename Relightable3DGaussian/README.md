# Relightable 3D Gaussian

This is the implementation of **Relightable 3D Gaussian** for the paper:

**Relightable 3D Gaussian: Real-time Point Cloud Relighting with BRDF Decomposition and Ray Tracing**

## Installation

### Clone the Repository
```bash
git clone https://github.com/NJU-3DV/Relightable3DGaussian.git
cd Relightable3DGaussian
```

### Install Dependencies
#### 1. Set up the Environment
```bash
conda env create --file environment.yml
conda activate r3dg
```

#### 2. Install PyTorch 1.12.1
```bash
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.6 -c pytorch -c conda-forge
```

#### 3. Install Additional Dependencies
```bash
pip install torch_scatter==2.1.1
pip install kornia==0.6.12
```

#### 4. Install NVidia Differentiable Rasterizer
```bash
git clone https://github.com/NVlabs/nvdiffrast
pip install ./nvdiffrast
```

## Configure CUDA Settings

### 1️⃣ Create a Conda Activation Script
Run the following inside your Conda environment:
```bash
mkdir -p $CONDA_PREFIX/etc/conda/activate.d
mkdir -p $CONDA_PREFIX/etc/conda/deactivate.d
```

### 2️⃣ Add CUDA Variables to the Activation Script
Create a new file for environment activation:
```bash
nano $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
```
Add the following lines:
```bash
#!/bin/bash
export CUDA_HOME=$CONDA_PREFIX
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_HOME/lib:$LD_LIBRARY_PATH
export CXXFLAGS="-std=c++14"
export FORCE_CUDA=1
```
Save the file (`CTRL+X`, then `Y`, then `ENTER`).

### 3️⃣ Create a Deactivation Script
To ensure CUDA settings revert when deactivating the environment, create a new file:
```bash
nano $CONDA_PREFIX/etc/conda/deactivate.d/env_vars.sh
```
Add the following:
```bash
#!/bin/bash
unset CUDA_HOME
unset PATH
unset LD_LIBRARY_PATH
unset CXXFLAGS
unset FORCE_CUDA
```
Save the file (`CTRL+X`, then `Y`, then `ENTER`).

## ✅ Step 2: Test the Environment Settings
Deactivate and reactivate your Conda environment:
```bash
conda deactivate
conda activate r3dg
```
Then check:
```bash
which nvcc
nvcc --version
```

## Install PyTorch Extensions
We recommend compiling the extensions with CUDA 11.8 to avoid potential issues.

```bash
# Install knn-cuda
pip install ./submodules/simple-knn

# Install BVH
pip install ./bvh

# Install Relightable 3D Gaussian
pip install ./r3dg-rasterization
```

