# SV-GaSRelight: Single-View Gaussian Splatting for 3D Human Relighting

This repository provides a pipeline for 3D human reconstruction and relighting using **3D Gaussian Splatting** from a single-view image. The implementation builds upon:

- [PSHuman](https://github.com/pengHTYX/PSHuman) for single-view 3D human reconstruction
- [Relightable 3D Gaussian](https://github.com/NJU-3DV/Relightable3DGaussian) for relighting with BRDF decomposition and real-time rendering

It leverages PyTorch and related deep-learning frameworks to achieve high-quality reconstruction and relighting.

---

## Installation

Follow the installation guides for each module:

- **[PSHuman Gaussian Installation](PSHuman/README.md)**  
  For single-view 3D reconstruction using PSHuman.

- **[Colmap to NeRF Transformation](TransformationFile/README.md)**  
  For generating `transforms.json` (camera parameters) from novel multiviews using PSHuman output.

- **[Relightable 3D Gaussian Installation](Relightable3DGaussian/README.md)**  
  For real-time relighting using BRDF decomposition and differentiable rasterization.

---

## Development Timeline

We are actively editing this repository to support our submission and the SV-GaSRelight paper. Below is the timeline of major updates:

| Date       | Update Description                                                                 |
|------------|--------------------------------------------------------------------------------------|
| 2025-04-19 | Initial repository setup using PSHuman and Relightable3DGaussian as base            |
| 2025-04-19 | Added installation guides and modular pipeline documentation                         |
| 2025-04-19 | Integrated `Colmap to NeRF Transformation` with example usage                        |
| 2025-04-19 | Refined README, fixed module paths, and cleaned up submodule integration             |
| *(ongoing)*| Adding relighting demo outputs, GUI launcher, and evaluation scripts                 |

---

## References

- [PSHuman Repository](https://github.com/pengHTYX/PSHuman)  
- [Relightable 3D Gaussian Repository](https://github.com/NJU-3DV/Relightable3DGaussian)  
- [Facebook Research - PyTorch3D](https://github.com/facebookresearch/pytorch3d)  
- [GraphDeco Inria - Diff Gaussian Rasterization](https://github.com/graphdeco-inria/diff-gaussian-rasterization)

---

## Contact

For questions, please reach out via the Issues tab or email at sonainjamil@ieee.org.
