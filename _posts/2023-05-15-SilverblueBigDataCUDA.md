---
title: Big Data and GPU acceleration with CUDA
date: 2023-05-15 00:00:00 +0000
categories: [Research, Linux]
---

Peer review process of earlier post. HPC for some of the workflows, but exploration benefits from local compute (agile).

Sawpfile usage as defined in earlier post.

sc omic public data. Needs integration. Possible with CCA or rPCA approaches. State of the art methods based on VAEs can benefit from GPU acceleration.

CUDA reguires of propietary NVIDIA driver. Installation in Silverblue not straigthforward due to particularities with rpm-ostree. If using pytorch and jax from conda environment, take care they can both access cuda install.
