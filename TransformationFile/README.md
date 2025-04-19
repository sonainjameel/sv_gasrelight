# Colmap to NeRF Transformation

This repository provides a modified version of `colmap2nerf.py` for converting COLMAP reconstructions to [NEILF](https://arxiv.org/abs/2203.07182)-compatible `transforms.json` format.

## Installation & Setup
To set up the environment and install COLMAP, follow these steps:
```sh
conda create -n colmap_env python=3.11 -y
conda activate colmap_env
conda install -c conda-forge colmap
```

Clone the required repository:
```sh
git clone https://github.com/NVlabs/instant-ngp.git
```

Copy the `colmap2nerf.py` to the appropriate COLMAP script directory:
```sh
cp colmap2nerf.py ~/colmap/scripts/python/
```

## Running COLMAP Reconstruction
Use the following commands to run the automatic reconstruction pipeline in COLMAP:
```sh
colmap automatic_reconstructor --workspace_path /home/user/TriplaneGaussian/outputs/video --image_path /home/user/TriplaneGaussian/outputs/video/0000_rgba
```
Convert the model to a text format:
```sh
colmap model_converter --input_path /home/user/TriplaneGaussian/outputs/video/sparse/0 --output_path /home/user/TriplaneGaussian/outputs/video/sparse/0 --output_type TXT
```


## Modifications in `colmap2nerf.py`
This modified version of `colmap2nerf.py` introduces the following changes:

- **Simplified JSON Output:** Removed unnecessary metadata fields, keeping only `file_path`, `rotation`, and `transform_matrix` in `transforms.json`.
- **Standardized Output Naming:** Converts filenames into a structured format (`test/000`, `test/001`, etc.) to ensure consistency.
- **Fixed Rotation Parameter:** A fixed rotation value (`0.031415926535897934`) is added to each frame.
- **Camera Metadata Cleanup:** Removed additional camera parameters (`k1, k2, cx, cy, etc.`) to match NEILF input requirements.
- **Improved Output Formatting:** Ensured JSON is written in a structured manner with `sort_keys=True` to maintain readability.
- **Scene Normalization:** Automatically adjusts scene orientation and scaling to align with NeRF's expectations.

## Running the Modified `colmap2nerf.py`
```sh
python ~/colmap/scripts/python/colmap2nerf2.py --text /home/user/TriplaneGaussian/outputs/video/sparse/0 --images /home/user/TriplaneGaussian/outputs/video/sparse/images --out /home/user/TriplaneGaussian/outputs/video/transforms3.json --aabb_scale 16
```

## License
This repository follows NVIDIA's licensing terms for the original `colmap2nerf.py` script. See the original repository for more details.

## Acknowledgments
- [COLMAP](https://colmap.github.io/)
- [Instant-NGP](https://github.com/NVlabs/instant-ngp)

