# BS-Diff: Effective Bone Suppression in CXRs via Conditional Diffusion Models

![](https://img.shields.io/badge/-Github-181717?style=flat-square&logo=Github&logoColor=FFFFFF)
![](https://img.shields.io/badge/-Awesome-FC60A8?style=flat-square&logo=Awesome&logoColor=FFFFFF)
![](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=Python&logoColor=FFFFFF)
![](https://img.shields.io/badge/-Pytorch-EE4C2C?style=flat-square&logo=Pytorch&logoColor=FFFFFF)

https://github.com/Benny0323/BS-Diff/blob/main/Display.mp4

## Proposed method 

We spend a lot of time collecting and summarizing relevant papers and datasets, where you can find them at https://github.com/diaoquesang/Diffusion_model-based_bone_suppression_in_chest_X-rays

This code is a pytorch implementation of our paper "BS-Diff: Effective Bone Suppression in CXRs via Conditional Diffusion Models", which is under review by ISBI2024.

Our proposed framework comprises **a conditional diffusion model (CDM) equipped with a U-Net architecture and a simple enhancement module** that incorporates an autoencoder with Kullback–Leibler divergence. It can not only generate soft tissue images with **a high bone suppression rate** but also possess the capability to **capture fine image details**. The first image below shows our provided method and the second image is the U-net architecture in our proposed network.

![image](https://github.com/Benny0323/BS/blob/main/BS-Diff.png)
![image](https://github.com/Benny0323/BS/blob/main/U-Net.png)

## The bone-suppressed images generated by our method
![image](https://github.com/Benny0323/BS/blob/main/contrast.png)

## Pre-requisties
* Linux

* Python>=3.7

* NVIDIA GPU (memory>=6G) + CUDA cuDNN

### Download the dataset
Now, we only provide three paired pictures with CXRs and soft-tissues. Soon, we will make them available to the public. They are located at
```
├─ Stage1
│    ├─ BS_Aug
│    │    ├─ 0.png
│    │    ├─ 1.png
│    │    └─ 2.png
│    ├─ CXR_Aug
│    │    ├─ 0.png
│    │    ├─ 1.png
│    │    └─ 2.png
```
## Getting started to evaluate
### Install dependencies
```
pip install -r requirements.txt
```
### Download the checkpoint
Due to the fact that our proposed model comprises two stages, you need to download both stages' checkpoints to successfully run the codes!
```
├─ Stage1
│    ├─ Aug_Final_ctrain.pth
└─ Stage2
     ├─ Aug_Hybrid_autoencoderkl.pth
```
### Evaluation
To do the evaluation process, first run the following command of stage 1 (the conditional diffusion model):
```
python Test.py
```      
Then, you will get a series of images generated by the conditional diffusion model. After that, run the following command of stage 2 with these images as inputs.
```
python Aug_Hybrid_autoencoderkleval.py
```
## Train by yourself
If you want to train our model by yourself, you can run the following command of stage 1:
```
python Train.py
```
Then after finishing stage 1, you can use the generated output of stage 1 to train our stage (enhancement module) by running the following command:
```
python Hybridloss_autoencoderkl.py
```
These two files are located at
```
├─ Stage1
│    └─ Train.py
└─ Stage2
     ├─ Hybridloss_autoencoderkl.py
     └─ pytorch_msssim.py
```
**Attention: the file 'pytorch_ssim.py' should be used during training in stage 2. So do not delete it!**

## Comparison metrics
You can also run our codes about PSNR, SSIM, MSE and BSR, which are located at
```
├─ Metrics
│    ├─ BSR.py
│    ├─ L2_loss.py
│    ├─ SSIM_PSNR.py
│    └─ resize.py
```
## Citation
