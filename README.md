# Comfyui_wafer

# Projects for text prompt engineering for SEM Wafer dataset

- Class-balancing loss for Dreambooth (with Lora-Training-in-Comfy)
- Text to image / Image to image
- IPAdapter
- Impainting
- IPAdapter with impainting
- ControlNet(Proceeding...)

# Class-balancing loss for Dreambooth (with Lora-Training-in-Comfy)

Based on Lora-Training-in-Comfy(https://github.com/LarryJane491/Lora-Training-in-Comfy/tree/main), I adjust "class-balanced loss"(, to train the long-tailed wafer defect dataset

Likewise Lora-Training-in-Comfy, the dataset (in 1 folder, containing all class of images, format in (
- dataset : Parent folder path of Path to long-tailed dataset,  
- beta_class_balancing : hyper-parameter for class-balancing loss, can be (0.9, 0.99, 0.999, 0.9999) referenced in original paper
- For head-class by multipling (1/Effective_number) with MSE loss, for tail-class by multiplying Effective number with prior-preserving loss

![Class-balancing LORA](https://github.com/mshdjren/Comfyui_wafer/blob/main/results/class_balanced_loss_Lora.jpg)

After installing, you can find it in the LJRE/LORA category or by double-clicking and searching for Training or LoRA.
Make sure you have a folder containing multiple images with captions.
Then, rename that folder into something like [number]_[whatever].
Copy the path of the folder ABOVE the one containing images and paste it in data_path. For example, if it's in C:/database/5_images, data_path MUST be C:/database.
Finally, just choose a name for the LoRA, and change the other values if you want. Then just click Queue Prompt and training starts!

I recommend using it alongside my other custom nodes, LoRA Caption Load and LoRA Caption Save:
![LoraCaption and Training](https://github.com/LarryJane491/Lora-Training-in-Comfy/assets/156431112/bd53593b-88f9-4a69-b4ff-5cad1b40294f)

That way you just have to gather images, then you can do the captioning AND training, all inside Comfy! And since it saves LoRAs in the loras folder of Comfy by default, you just need to refresh and you can test it right away!

Results from the first LoRA I got with my method:

![w62yekl73obc1](https://github.com/LarryJane491/Lora-Training-in-Comfy/assets/156431112/480b5b7b-d6af-4472-a476-8f2fb94dfe0e)
![am585t5h3obc1](https://github.com/LarryJane491/Lora-Training-in-Comfy/assets/156431112/0acad9ef-23c0-490b-a2c0-f65fdfc4f1ad)
![1wacnvrv5obc1](https://github.com/LarryJane491/Lora-Training-in-Comfy/assets/156431112/9fbe23da-fee1-4107-be00-d726bcf9bd07)


You can compare with real images:
https://www.google.com/search?client=opera&hs=eLO&sca_esv=597261711&sxsrf=ACQVn0-1AWaw7YbryEzXe0aIpP_FVzMifw:1704916367322&q=Pokemon+Dawn+Grand+Festival&tbm=isch&source=lnms&sa=X&ved=2ahUKEwiIr8izzNODAxU2RaQEHVtJBrQQ0pQJegQIDRAB&biw=1534&bih=706&dpr=1.25



IMPORTANT NOTES:
This node is confirmed to work for SD 1.5, SD2.0, SDTurbo and LCM.
But I have no idea about SDXL. If someone could test it and confirm or infirm, I’d appreciate ^^. I know the LoRA project included custom scripts for SDXL, so maybe it’s more complicated.

----

TROUBLESHOOT:
The very first version I published online had very strict requirements, which made conflicts likely. I've reduced requirements to the bare minimum, but conflicts can still arise. If that happens to you, please let me know!

"No module X found" : This error happens when Python can't find the required modules for the running program. For ComfyUI, it often happens if you forgot to install requirements for the custom node.
But it can also happen if you installed the requirements in the wrong folder! If your ComfyUI folder has a virtual environment (venv), make sure to enable it before installing requirements.


"Something about cuda.dll missing" : there's a lot of variants of this error, but they're all the same problem (hopefully): it happens if you haven't installed CUDA properly (or, again, if it's not installed in the right folder). Here is what to do in this case:
1) Open a command prompt and make absolutely sure that it's the right environment.
2) Go there: https://pytorch.org and scroll down. Follow the instructions to get a line of code, something like pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121. Copy-paste the line the website gives you into the command prompt you opened and press Enter. This will install CUDA.



I own a Windows 10 machine with a RTX 3060. I can't test for Linux, for MAC, for AMD GPUs and other weird situations x).




----

TO GO FURTHER
Even the Advanced node doens't include all inputs available for LoRA training, but you can find them all in the script train.py! All of that can be modified by the user directly within the script.


----
SHOUTOUT
This is based off an existing project, lora-scripts, available on github. Thanks to the author for making a project that launches training with a single script!

I took that project, got rid of the UI, translated this “launcher script” into Python, and adapted it to ComfyUI. Still took a few hours, but I was seeing the light all the way, it was a breeze thanks to the original project ^^.
