# Comfyui_wafer

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
- beta_class_balancing : hyper-parameter for class-balancing loss, can be (0.9, 0.99, 0.999, 0.9999) referenced in original paper
- For head-class by multipling (1/Effective_number) with MSE loss, for tail-class by multiplying Effective number with prior-preserving loss

## Effective Number 정의
Effective Number는 클래스 내 샘플의 정보량을 측정하는 지표로, 다음과 같이 계산됩니다:

\[
E(n) = \frac{1 - \beta^n}{1 - \beta}
\]

- \(n\): 해당 클래스의 샘플 수
- \(\beta \in [0, 1)\): 하이퍼파라미터로, 클래스 간 균형 정도를 조정합니다.

샘플 수가 많아질수록 정보 간 중복이 증가하여 모델이 얻을 수 있는 새로운 정보량이 감소합니다. 이를 반영해 Effective Number를 계산합니다.

## Class-Balanced Loss 수식
각 클래스의 Effective Number에 반비례하는 가중치를 손실 함수에 곱하여 Class-Balanced Loss를 정의합니다:

\[
CB(p, y) = \frac{1 - \beta}{1 - \beta^{n_y}} L(p, y)
\]

- \(p\): 모델이 예측한 클래스 확률
- \(y\): 실제 클래스 레이블
- \(n_y\): 실제 클래스 \(y\)의 샘플 수
- \(L(p, y)\): 기본 손실 함수 (예: CrossEntropyLoss, FocalLoss 등)

### 주요 특징
1. **가중치 계산**:
   \[
   \alpha_i = \frac{1 - \beta}{1 - \beta^{n_i}}
   \]
   여기서 \(n_i\)는 클래스 \(i\)의 샘플 수입니다.

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
