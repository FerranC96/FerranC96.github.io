---
title: Big -omic Data and GPU acceleration with CUDA
date: 2023-05-15 00:00:00 +0000
categories: [Research, Linux]
---

Peer review process of earlier post. HPC for some of the workflows, but exploration benefits from local compute (agile).

Sawpfile usage as defined in earlier post.

sc omic public data. Needs integration. Possible with CCA or rPCA approaches. State of the art methods based on VAEs can benefit from GPU acceleration.

CUDA reguires of propietary NVIDIA driver. Installation in Silverblue not straigthforward due to particularities with rpm-ostree. If using pytorch and jax from conda environment, take care they can both access cuda install.


As part of the peer-review process of Cardoso Rodriguez & Qin et al. 2023, we decided to compare our murine organoid data with publicly available patient cohorts of Colorectal Cancer. While some of the workflows were suited for the HPC, dataset exploration benefits from the agility of local compute. 
Now, with Variational AutoEncoder approaches for data integration implemented in PyTorch, my laptop's GPU was more than adequate for this.


### Utilizing CUDA for -omic Data Integration:

To integrate single-cell (sc) -omic public data, methods such as Canonical Correlation Analysis (CCA) or Robust Principal Component Analysis (rPCA) can be employed. State-of-the-art techniques based on Variational Autoencoders (VAEs) can benefit significantly from GPU acceleration provided by CUDA. However, CUDA requires the installation of the proprietary NVIDIA driver, which might not be straightforward in Silverblue due to the unique characteristics of rpm-ostree. If using PyTorch and JAX from a Conda environment, care must be taken to ensure both frameworks can access the CUDA installation.


#### Installing the NVIDIA Driver:

To install the NVIDIA driver, follow the instructions provided by RPM Fusion: https://rpmfusion.org/Howto/NVIDIA#OSTree_.28Silverblue.2FKinoite.2Fetc.29. On Silverblue, a hack is required to load the proprietary NVIDIA driver. In some cases, it may be necessary to lower the secure boot settings or disable it completely. Additional information can be found in the following GitHub repository: https://github.com/CheariX/silverblue-akmods-keys.

### Increasing Swap for Big CRC Datasets:

To handle large CRC datasets effectively, increasing the swap size is crucial. Long time usage (abuse really) will murder your disk longevity, but it does sure come convenient in a pinch!

Use the following command to create a 64GB swap file:

`btrfs filesystem mkswapfile --size 64G $swapfile`

Activate the swap file with the following command:

`sudo swapon $swapfile`

This can be automatically activated at boot too, but I only use it when working with Big Data locally.

### Setting up scvi-tools with CUDA on Linux:

When installing scvi-tools through Conda, JAX cannot utilize CUDA unless you also install cuda-nvcc. Run the following command after installing PyTorch, CUDA, and other dependencies through Conda:

`conda install jax cuda-nvcc -c conda-forge -c nvidia`

Next, install scvi-tools, Scanpy, and scikit-misc:

`conda install scvi-tools scanpy scikit-misc -c conda-forge`

If encountering issues, you can try creating a new empty environment and installing the necessary packages using mamba:

`mamba create -n myenv python=3.9`
`conda activate myenv`
`mamba install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia`
`mamba install jaxlib jax cuda-nvcc -c conda-forge -c nvidia`
`conda install scvi-tools scanpy scikit-misc -c conda-forge`
