# Frequency-Aware Fine-Tuning of SwinIR-Light for 4x Single Image Super-Resolution

This repository contains the implementation materials for the final term project:

**Frequency-Aware Fine-Tuning of SwinIR-Light for 4x Single Image Super-Resolution Using Hann-Windowed Spectral Magnitude Regularization**

## Overview

This project investigates whether frequency-domain supervision can improve single image super-resolution results without changing the inference architecture of the model.

The study uses the official pretrained SwinIR-Light model as the backbone. The proposed model is fine-tuned using a Hann-windowed FFT magnitude regularization term in addition to the standard L1 reconstruction loss.

The FFT branch is used only during training and introduces no additional inference-time parameters.

## Method

The final proposed model is referred to as **A1**.

The training objective is:

```text
Total Training Loss = L1 Loss + 0.10 * FFT Loss
```

The FFT loss is computed by:

1. Applying a 2D Hann window to the super-resolved and ground-truth images.
2. Computing the 2D FFT.
3. Comparing the log-magnitude spectra using an L1 distance.

## Compared Models

| Model | Description |
|---|---|
| Bicubic | Non-learning interpolation baseline |
| Official SwinIR-Light | Official pretrained SwinIR-Light model |
| A0 | SwinIR-Light fine-tuned using L1 loss only |
| A1 | SwinIR-Light fine-tuned using L1 loss and Hann-windowed FFT magnitude regularization |

Pilot ablation experiments also evaluated:

| Model | Description |
|---|---|
| A2 | L1 loss with Laplacian edge regularization |
| A3 | L1 loss with FFT and Laplacian edge regularization |

## Datasets

The project uses:

- DIV2K Train for fine-tuning
- DIV2K Validation for ablation and checkpoint selection
- Set5, Set14, BSDS100, Urban100, and Manga109 for external benchmark evaluation

The datasets are not included in this repository and should be obtained from their official sources or from the Kaggle dataset environment used during the project.

## Evaluation Metrics

The models were evaluated using:

- PSNR-Y
- SSIM-Y
- LPIPS-RGB
- FSIM
- HF-LSE
- Reconstruction time

HF-LSE means high-frequency log-spectrum error and measures the difference between the reconstructed and ground-truth images in the high-frequency spectral domain.

## Main Results

Compared with the L1-only A0 control model, the proposed A1 model achieved the following macro-average results across Set5, Set14, BSDS100, Urban100, and Manga109:

| Metric | Result |
|---|---|
| HF-LSE improvement | 1.55% |
| LPIPS-RGB improvement | 1.28% |
| PSNR-Y change | -0.0120 dB |
| SSIM-Y change | +0.000007 |

These results show that Hann-windowed FFT regularization improves spectral and perceptual fidelity while preserving nearly the same distortion-level reconstruction quality.

## Repository Contents

```text
notebooks/
    final_project_notebook.ipynb

results/
    complete_all_five_benchmarks_summary.csv
    final_A1_vs_A0_all_benchmarks.csv
    selected_visual_examples.csv

figures/
    fig1_workflow.png
    urban100_img054_crop_comparison.png
    urban100_img054_error_comparison.png
    manga109_thatsizumiko000_crop_comparison.png
```

## Requirements

The project was implemented in Python using PyTorch in a Kaggle GPU runtime.

Main libraries:

```text
torch
torchvision
numpy
pandas
Pillow
opencv-python
scikit-image
matplotlib
tqdm
lpips
piq
timm
```

## Notes

Large datasets and model checkpoints may not be included in this repository due to file size limitations. The notebook and result files document the experimental workflow and final evaluation results.

## AI Tool Usage

AI-based assistance tools were used during the preparation of this study. ChatGPT was used to support code debugging, experimental workflow organization, numerical result checking, and language refinement. Gemini was used to obtain feedback on the clarity, consistency, and structure of drafted report sections. All experimental executions, dataset handling, methodological decisions, result interpretations, and final scientific conclusions were reviewed, verified, and finalized by the author.

## Author

Kadriye Elif Yavuz  
Abdullah Gul University  
Department of Electrical and Electronics Engineering
