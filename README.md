// ...existing code...
# Astronomical Image Denoising using SwinIR

A Swin Transformer based image restoration project for astronomical image denoising.

## Contents
- [SwinIR_Denoising.ipynb](SwinIR_Denoising.ipynb) — training, evaluation, and visualization notebook.  
- [img_download.ipynb](img_download.ipynb) — helper notebook to download SDSS images from coordinates.  
- [README.md](README.md) — this file.

## Overview
This repository demonstrates training a Swin Transformer based denoising model on astronomical image pairs (noisy / clean). The core model and dataset utilities are implemented in the training notebook. Key notebook symbols:
- [`SwinIR`](SwinIR_Denoising.ipynb) — model class definition  
- [`AstroDenoiseDataset`](SwinIR_Denoising.ipynb) — dataset class / data loading  
- [`PerceptualLoss`](SwinIR_Denoising.ipynb) — perceptual loss (VGG-based)  
- [`copy_images`](SwinIR_Denoising.ipynb) — helper used for dataset split / copying  
- [`compute_psnr`](SwinIR_Denoising.ipynb) — evaluation metric helper  
- [`visualize_sample_predictions_with_metrics`](SwinIR_Denoising.ipynb) — visualization helper

## Quickstart

1. Open and run:
   - Training / eval: [SwinIR_Denoising.ipynb](SwinIR_Denoising.ipynb)  
   - Data download: [img_download.ipynb](img_download.ipynb)

2. Typical workflow:
   - Use [img_download.ipynb](img_download.ipynb) to fetch SDSS image tiles (configure CSV with ra/dec).
   - Prepare aligned noisy/clean pairs and run the dataset split / copy step in [SwinIR_Denoising.ipynb](SwinIR_Denoising.ipynb).
   - Configure device, hyperparameters, and run the training cells. Checkpoints are saved periodically (e.g. `swinir_sdss_denoise_checkpoint_ep{n}.pth`) and final weights saved as `swinir_sdss_denoise_final.pth`.

## Requirements
- Python 3.8+  
- PyTorch (GPU recommended)  
- torchvision, timm, pytorch-msssim, PIL, tqdm, scikit-image, matplotlib, numpy, pandas, requests

Exact install commands are included in the notebooks.

## Training & Evaluation
- Training loop, checkpointing, and logging are implemented inside [SwinIR_Denoising.ipynb](SwinIR_Denoising.ipynb).  
- Use the notebook cell that defines the optimizer and loss (AdamW + perceptual loss) to reproduce experiments.
- Evaluation uses PSNR / SSIM (helpers in the notebook: [`compute_psnr`](SwinIR_Denoising.ipynb), `ssim`).

## Inference / Visualization
- Use `visualize_sample_predictions_with_metrics` in [SwinIR_Denoising.ipynb](SwinIR_Denoising.ipynb) to generate side-by-side noisy / prediction / ground-truth figures and compute PSNR/SSIM.

## Data layout (expected)
- /content/aligned/train/clean  
- /content/aligned/train/noisy  
- /content/aligned/test/clean  
- /content/aligned/test/noisy

The notebook includes helpers to create these folders and copy splits via [`copy_images`](SwinIR_Denoising.ipynb).

## Notes
- Notebooks contain logs showing training progress and checkpoint saves (e.g., `✅ Checkpoint saved: swinir_sdss_denoise_checkpoint_epXX.pth`).
- Adjust image transforms and normalization when switching datasets or image sizes.

## Contact
For questions about the project contact the original author (see
