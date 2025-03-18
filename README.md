# Comfyui_wafer

# Projects for text prompt engineering for SEM Wafer dataset

- Class-balancing loss for Dreambooth (with Lora-Training-in-Comfy)
- Text to image / Image to image
- IPAdapter
- Impainting
- IPAdapter with impainting
- ControlNet(Proceeding...)

# Class-balancing loss for Dreambooth (with Lora-Training-in-Comfy)

Based on [Lora-Training-in-Comfy](https://github.com/LarryJane491/Lora-Training-in-Comfy/tree/main), I adjust "class-balanced loss"(, to train the long-tailed wafer defect dataset

Likewise Lora-Training-in-Comfy, the dataset (in 1 folder, containing all class of images, format in (
- dataset : Parent folder path of Path to long-tailed dataset,  
- beta_class_balancing : hyper-parameter for class-balancing loss, can be (0.9, 0.99, 0.999, 0.9999) referenced in original paper
- For head-class by multipling (1/Effective_number) with MSE loss, for tail-class by multiplying Effective number with prior-preserving loss

![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/class_balanced_loss_Lora.jpg)


# Text to image / Image to image


![Text to image](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/SDXL_text2image.jpg)]

# IPAdapter

![IPAdapter](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/SDXL_IPAdapter.jpg)

# Impainting

# IPAdapter with impainting


----

TO GO FURTHER
# ControlNet(Proceeding...)


----
