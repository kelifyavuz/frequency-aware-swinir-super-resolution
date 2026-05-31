# Frequency-Aware Fine-Tuning of SwinIR-Light for 4x Single Image Super-Resolution

This repository contains the implementation and experimental materials for the final term project:

**Frequency-Aware Fine-Tuning of SwinIR-Light for 4x Single Image Super-Resolution Using Hann-Windowed Spectral Magnitude Regularization**

## Project Overview

This project investigates whether frequency-domain supervision can improve the reconstruction behavior of a transformer-based single image super-resolution model without changing its inference architecture.

The study uses the official pretrained SwinIR-Light model as a fixed backbone and fine-tunes it with a Hann-windowed FFT magnitude regularization term. The proposed model is compared with bicubic interpolation, the official pretrained SwinIR-Light baseline, and an L1-only fine-tuned control model.

## Method Summary

The final proposed model, referred to as A1, uses the following training objective:

```text
Total Training Loss = L1 Loss + 0.10 * FFT Loss
