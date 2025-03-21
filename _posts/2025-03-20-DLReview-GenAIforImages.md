---
title: "DLReview_Day1 : Generative AI for Images "
excerpt: " VAEs and GANs / how diffusion models are trained and sampling is conducted to generate image"

categories:
  - 📚 Deep Learning
tags:
  - [DLReview, Diffusion Model]

permalink: /📚 Deep Learning/post-name-here/

toc: true
toc_sticky: true

date: 2025-03-20
last_modified_at: 2025-03-20
---

## 🦥 DLReview_Day1 : Generative AI for Images 

### 1️⃣ Supervised Learning & Unsupervised Lerning 

### 2️⃣ 3 deep-learning based generative models

- **Autoencoder** 
- **Variational autoencoder**
- **Generative adversarial networks**

### Autoencoder 


---

### VAE 

<img width="521" alt="image" src="https://github.com/user-attachments/assets/c5c926ab-0b59-4558-a53f-3ed687f75604" />
    
    
    - the end of the encoder you are going to get really densed one. 
    - can connect to decoder 
    - it is able to reproduce original image 
    - at z factor, we can extract (compressing) / using MSE means 


onec we train we have z, all we can do is twicking it all of it and generate it someting similar 
How can we twick the z ( z is long vector) 

#### How can we introduce some ‘randomness’ into the generation process?

- Instead of learning the latent vectors directly, can we learn the
distribution of each element? = approximate with mean 𝜇𝜇 and standard deviation
- We assume the distributions are Norma



#### How VAE Works 
  1. **Encoder**
     - Take input data (ex.image) and compresses it into a latent representation.
     - Outputs two values: mean (μ) and standard deviation (σ), which define the distribution of the latent variable z

       ✅ latent representation : compressing data and only taking important data 
 
  2. **Sampling**
      - Samples the latent variable z from the distribution defined by μ and σ
      - This adds randomness, allowing the generation of diverse outputs
 
  3. **Decoder**
       - Take the sampled latent variable z and reconstructs the original data (ex.an image)
       - 
  5. **Lossfunction** : 

       - ✅ reparameterization : it is part of the encoder since it is before Z
---

### GANs
- One of the Genertive model that can create realistic fake data. 
- The idea of Gans is concept that one model is **Generator** and another is **Discriminator**
- Main Components of GANs : **Generator** , **Discriminator**
  #### **Generator** :
  >####                - Generate fake data from random noise.
  >####                - Its goal is to generate data that looks real

 #### **Discriminator** :
  >####                - Judge whther the input is real of fake.
  >####                - Its goal is to accurately distinguish between real and fake data

 📌 They are doing competition,both networks improve over time through this competition.


---


**What is noise?**
- The set of randon generated numbers ex) [0.1,-0.3,0.8,0.2]
- The number are provided generally from normal distribution or uniform distribution. 
- 노이즈는 generator에게 "여기서 시작해서 무언가 만들어봐!"라고 알려주는 역할을 한다.

**Why we need noise?**
- Providing startpoint : Generator makes a image based on the information of noise. If there is no noise, generator doesn't know where to start.
- making diversity :generators use diffiernt noise each time, allowing them to create a variety of images. For example, even when drawing the same dog, different noise can result in different appearances of the dog.
- giving creativity : Different noise helps generator create entirely new images. 
  






