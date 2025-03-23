# Defect Text Prompt Engineering Projects for SEM Wafer Dataset

## Overview
This repository contains projects focused on text prompt engineering and image generation using the SEM Wafer dataset. The main objectives are:

- Addressing class imbalance with Class-Balanced Loss for Dreambooth (using LoRA Training in ComfyUI)
- Generating images via Text-to-Image and Image-to-Image
- Domain adaptation using IPAdapter and Inpainting
- Exploring ControlNet (Work in Progress)

## Class-Balanced Loss for Dreambooth

Based on [Lora-Training-in-Comfy](https://github.com/LarryJane491/Lora-Training-in-Comfy/tree/main), I adjust [class-balanced loss](https://arxiv.org/pdf/1901.05555), to train the long-tailed wafer defect dataset.

- Dataset Path: Parent folder path to the long-tailed dataset.
The dataset is organized in a single folder containing all classes of images, formatted as "[class_name]_[img0].png".

## Adapting Class-Balanced Loss for Dreambooth
Class-balanced loss and Effective Number are defined as follows:
![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/loss.png)
![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/samples.png)

n: Number of samples in a class
β: Hyperparameter for class balancing (e.g., 0.9, 0.99, 0.999, 0.9999).

Implementation:
For head classes: MSE loss is scaled by 1/E(n).
For tail classes: Prior-preserving loss is scaled by E(n)

![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/class_balanced_loss_details.jpg)

Prompt Structure:[Domain type][Defect prefix][Image description]
Positive Prompts: scanning electron microscope, defect, ring-shaped, solo, centered, concentric rings, jagged edges, smooth outer boundary, metallic texture, monochrome, greyscale, high-resolution, no humans, close-up, uniform background, fine-grain texture.

Negative Prompts: colorized, blurry, low quality, distorted shapes, extra patterns, uneven textures, unrealistic proportions, overexposed areas, grainy noise, missing defect, missing contrast, artifacts, poor lighting.

![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/class_balanced_loss_Lora.jpg)


# Text-to-Image / Image-to-Image
For text-to-image generation using SDXL:

Three text prompt sources were tested: WDTagger, LLAMA 3.2, and GPT-4.5.

GPT-4.5 prompts produced the best results for SEM wafer images with ring-type defects.

Challenges:
SEM wafer images differ significantly from the domain of pre-trained SDXL models, making precise defect generation difficult.

![Text to image](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/SDXL_text2image.jpg)

# IPAdapter
To address the domain gap between SEM wafer images and pre-trained SDXL models:

IPAdapter with Input Images: Achieved better results than naive text-to-image generation.

Normal Pattern Similarity: Maintaining normal patterns is crucial in anomaly detection since deviations from normal patterns are identified as defects.

![IPAdapter](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/SDXL_IPAdapter.jpg)

Generate only defect regions while preserving normal patterns using inpainting techniques.

# Impainting
Before applying inpainting with IPAdapter:

Naive text prompts were used to generate defect regions without IPAdapter.

Similar to text-to-image results, generating precise defect regions solely with text prompts proved challenging.

Preferred prompts were sourced from GPT-4.5.

# IPAdapter with Inpainting
Combining IPAdapter and inpainting techniques yielded optimal results:

Preserved normal patterns from input images.

Generated defect regions using SDXL with IPAdapter-guided prompts.

TO GO FURTHER
# ControlNet (Work in Progress)
