# SV-GaSRelight: Single-View Gaussian Splatting for 3D Human Relighting

This repository provides a pipeline for 3D human reconstruction and relighting using **3D Gaussian Splatting** from a single-view image. The implementation is based on [PSHuman](https://github.com/pengHTYX/PSHuman) and [Relightable 3D Gaussian](https://github.com/NJU-3DV/Relightable3DGaussian). It leverages PyTorch and related deep-learning frameworks to achieve high-quality relighting and reconstruction.

## Installation

Follow the installation guides for each module:

- **[PSHuman Gaussian Installation](PSHuman/Readme.md)**: For single-view 3D reconstruction using PSHuman.
- **[Colmap to NeRF Transformation](TransformationFile/README.md)**: For generating transform.jason file from the novel multiviews using PSHuman.
- **[Relightable 3D Gaussian Installation](Relightable3DGaussian/README.md)**: For real-time relighting using BRDF decomposition and ray tracing.

## References

- [PSHuman Repository](https://github.com/pengHTYX/PSHuman)
- [Relightable 3D Gaussian Repository](https://github.com/NJU-3DV/Relightable3DGaussian)
- [Facebook Research - PyTorch3D](https://github.com/facebookresearch/pytorch3d)
- [GraphDeco Inria - Diff Gaussian Rasterization](https://github.com/graphdeco-inria/diff-gaussian-rasterization)

