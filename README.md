<img width="626" alt="image" src="https://github.com/user-attachments/assets/d26ab42d-c4e7-49a1-80e4-c6c587a2a714" /># Comfyui_wafer

# Projects for text prompt engineering for SEM Wafer dataset

- Class-balancing loss for Dreambooth (with Lora-Training-in-Comfy)
- Text to image / Image to image
- IPAdapter
- Impainting
- IPAdapter with impainting
- ControlNet(Proceeding...)

# Class-balancing loss for Dreambooth (with Lora-Training-in-Comfy)

Based on [Lora-Training-in-Comfy](https://github.com/LarryJane491/Lora-Training-in-Comfy/tree/main), I adjust [class-balanced loss](https://arxiv.org/pdf/1901.05555), to train the long-tailed wafer defect dataset

Likewise Lora-Training-in-Comfy, the dataset (in 1 folder, containing all class of images, format in "[class_name]_[img0].png"
- dataset : Parent folder path of Path to long-tailed dataset,  

## Adapting class balanced loss for dreambooth, Effective Number 정의
Class-balanced loss & Effective Number can be defined as follows, (beta_class_balancing : hyper-parameter for class-balancing loss, can be (0.9, 0.99, 0.999, 0.9999) referenced in original paper)
and i applied class balancing loss differently for MSE loss & prior-preserving loss
![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/loss.png)
![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/samples.png)

- For head-class by multipling (1/Effective_number) with MSE loss, for tail-class by multiplying Effective number with prior-preserving loss as follows
![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/class_balanced_loss_details.jpg)

![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/class_balanced_loss_Lora.jpg)


# Text to image / Image to image
To naive text-to-image SDXL, i use 3 different text prompt from wdtagger, LLAMA 3.2, gpt4.5
experiencely, i prefer prompt from gpt 4.5
For example temx prompt in workflow SEM wafer image(ring-type defect),
- Text prmopt : 

but, SEM wafer has totally different domain with pretrained SDXL, it's not easy to generate precise defect SEM wafer 

![Text to image](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/SDXL_text2image.jpg)

# IPAdapter
To bridge the domain gap between SEM wafer and pretrained SDXL, IPAdapter with load image had a better image than naively use text to image SDXL

but, noraml pattern similiarity also can be important (which mainly defined as normal image in anomaly detection & totally different normal pattern would be seen as defect pixel in normal pattern distributio),
i'd like to utilize generate only defect part, maintaining the noraml pattern by impainting techinque.
![IPAdapter](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/SDXL_IPAdapter.jpg)

# Impainting
Before adapting impainting with IPAdapter, we simply confirm the naively text prompt to generate defect part, w/o IPAdapter
Likewise in text2image results, it's not easy to generate precise defect part with only text prompt (in this case, i'd also prefer text prompt from gpt4.5)

# IPAdapter with impainting
Consider all this prompt setting from above, i think this is the best selection for, 
- maintaining the normal pattern part from load image
- impainting only the defect part, by generating defect from pretrained SDXL, with prompt knowledge from IPAdapter
----

TO GO FURTHER
# ControlNet(Proceeding...)


----
