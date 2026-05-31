Set up of https://github.com/JianlingWANG2021/SGSST/tree/main with uv

Specs that works:

- Cuda 11.6
- Ubuntu 20.04

## Clone the repo 

```
git clone https://github.com/nghochi123/tmp_share.git --recurse-submodules
```

## Set up the venv

```
uv sync
```

## Install submodules (not built with uv)

```
uv pip install submodules/diff-gaussian-rasterization submodules/simple-knn --no-build-isolation
```

## Download the VGG weights

```
import gdown
gdown.download("https://drive.google.com/uc?id=1lLSi8BXd_9EtudRbIwxvmTQ3Ms-Qh6C8", "scaling_painting_style_transfer/model/vgg_conv.pth")
```

## Download the datasets

I use this one: https://drive.google.com/drive/folders/1l45X5sgjf134KRJkyiXLnPvL4RBIz45l

## Run the train, stylize, and render

```python
# Train
python train.py --source_path ./TanksAndTemples/Family/ --model_path ./model/output --resolution 1 --iterations 5000 --checkpoint_iterations 5000
# Stylize
python stylize.py --source_path ./TanksAndTemples/Family/ --model_path ./model/output_stylized --start_checkpoint ./model/output/chkpnt5000.pth --style_img ./styles_imgs/1.jpg --iterations 10000 --checkpoint_iterations 10000 --resolution 1
# Render
python render.py ./model/output_stylized/ --source_path ./TanksAndTemples/Family/
```
