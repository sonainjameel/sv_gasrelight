# PSHuman

This is the official implementation of *PSHuman: Photorealistic Single-image 3D Human Reconstruction using Cross-Scale Multiview Diffusion*.

### [![Project Page](https://raw.githubusercontent.com/prs-eth/Marigold/main/doc/badges/badge-website.svg)](https://penghtyx.github.io/PSHuman/) | [![Paper](https://img.shields.io/badge/arXiv-PDF-b31b1b)](https://arxiv.org/pdf/2409.10141) | [![Demo](https://img.shields.io/badge/🤗%20Hugging%20Face%20-Space-yellow)](https://huggingface.co/spaces/fffiloni/PSHuman) | [![Hugging Face Model](https://img.shields.io/badge/🤗%20Hugging%20Face%20-Model-green)](https://huggingface.co/pengHTYX/PSHuman_Unclip_768_6views) 

https://github.com/user-attachments/assets/b62e3305-38a7-4b51-aed8-1fde967cca70

https://github.com/user-attachments/assets/76100d2e-4a1a-41ad-815c-816340ac6500


Given a single image of a clothed person, **PSHuman** facilitates detailed geometry and realistic 3D human appearance across various poses within one minute.

### 📝 Update
- __[2024.11.30]__: Release the SMPL-free [version](https://huggingface.co/pengHTYX/PSHuman_Unclip_768_6views), which does not require SMPL condition for multiview generation and perform well in general posed human.
- __[2024.12.11]__: The huggingface demo has been deployed [here](https://huggingface.co/spaces/fffiloni/PSHuman). Special thanks to [Sylvain Filoni](https://github.com/fffiloni)! Take a try now.

### Common issues
- **Q:** Minimum VRAM requirement  
**A**: The current model is trained at a resolution of 768, requiring over 40GB of VRAM. We are considering training a new model at a resolution of 512, which would allow it to run on an RTX 4090.

### Installation
```
conda create -n pshuman python=3.10
conda activate pshuman

# torch
pip install torch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 --index-url https://download.pytorch.org/whl/cu121

# kaolin
pip install kaolin==0.17.0 -f https://nvidia-kaolin.s3.us-east-2.amazonaws.com/torch-2.1.0_cu121.html

# other dependency
pip install -r requirements.txt
```

This project is also based on SMPLX. We borrowed the related models from [ECON](https://github.com/YuliangXiu/ECON) and [SIFU](https://github.com/River-Zhang/SIFU), and re-organized them, which can be downloaded from [Onedrive](https://hkustconnect-my.sharepoint.com/:u:/g/personal/plibp_connect_ust_hk/EZQphP-2y5BGhEIe8jb03i4BIcqiJ2mUW2JmGC5s0VKOdw?e=qVzBBD). 



### Inference
1. Given a human image, we use [Clipdrop](https://github.com/xxlong0/Wonder3D?tab=readme-ov-file) or ```rembg``` to remove the background. For the latter, we provide a simple scrip.
```
python utils/remove_bg.py --path $DATA_PATH$
```
Then, put the RGBA images in the ```$DATA_PATH$```.

2. By running [inference.py](inference.py), the textured mesh and rendered video will be saved in ```out```.
```
CUDA_VISIBLE_DEVICES=$GPU python inference.py --config configs/inference-768-6view.yaml \
    pretrained_model_name_or_path='pengHTYX/PSHuman_Unclip_768_6views' \
    validation_dataset.crop_size=740 \
    with_smpl=false \
    validation_dataset.root_dir=$DATA_PATH$ \
    seed=600 \
    num_views=7 \
    save_mode='rgb' 

``` 
You can adjust the ```crop_size``` (720 or 740) and ```seed``` (42 or 600) to obtain best results for some cases.  

### Training
For the data preparing and preprocessing, please refer to our [paper](https://arxiv.org/pdf/2409.10141). Once the data is ready, we begin the training by running
```
bash scripts/train_768.sh
```
You should modified some parameters, such as ```data_common.root_dir``` and ```data_common.object_list```.

### Related projects
We collect code from following projects. We thanks for the contributions from the open-source community!     

[ECON](https://github.com/YuliangXiu/ECON) and [SIFU](https://github.com/River-Zhang/SIFU) recover human mesh from single human image.   
[Era3D](https://github.com/pengHTYX/Era3D) and [Unique3D](https://github.com/AiuniAI/Unique3D) generate consistent multiview images with single color image.  
[Continuous-Remeshing](https://github.com/Profactor/continuous-remeshing) for Inverse Rendering.


### Citation
If you find this codebase useful, please consider cite our work.
```
@article{li2024pshuman,
  title={PSHuman: Photorealistic Single-view Human Reconstruction using Cross-Scale Diffusion},
  author={Li, Peng and Zheng, Wangguandong and Liu, Yuan and Yu, Tao and Li, Yangguang and Qi, Xingqun and Li, Mengfei and Chi, Xiaowei and Xia, Siyu and Xue, Wei and others},
  journal={arXiv preprint arXiv:2409.10141},
  year={2024}
}
```
