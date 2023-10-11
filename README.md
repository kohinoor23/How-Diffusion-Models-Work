# How-Diffusion-Models-Work
Notes from How Diffusion Models Work by DeepLearning.ai

### Contents
#### Intuition
#### Sampling    

   - With Extra Noise 


https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/9b44015b-2c15-47af-81e8-12fd2592449d

#### Training

#### Context Embedding

#### Faster Sampling
---
## Notes
> Taught By Sharon Zhou 

> Noted by Atul

- Missing Prerequisite: [Backprop](https://www.youtube.com/watch?v=tIeHLnjs5U8)
<p align = "center">
<img width="487" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/a41ae493-ed32-4dd2-9bfd-b2b78ecd76f3">
</p>

- Example used throughout the course: Generate 16X16 size sprites for video games.

## Intuition
- Goal : Given a lot of sprite images, generate even more sprite images
<p align = "center">
  <img width="260" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/148e026a-7d15-4bbf-96ef-ee2fc68f01fa">
</p> 

- What does the network learn?
    - Fine details
    - General outline
    - Everything in between

- _Noising Process_  (bob as ink drop analogy)
<img width="483" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/b16289e8-e954-4c1b-9cda-27e2956ef1ec">

- _Denoising Process_ (what should the NN think?)
    - If its' Bob the sprite, keep it as it is
    - If its likely to be Bob, suggest more details to be filled
    - If its just an outline of a sprite, suggest general details for likely sprite(bob/fred/...)
    - If its nothing, suggest outline of a sprite

- Give the NN input noise, whose pixels are obtained from Normal distribution, and get a completely new sprite !

## Sampling
- Assume you have a trained NN
- At each denoising step, **it predicts noise**, and subtracts it to get a better image
- NOTE: At each denoising step, some random noise is added again to prevent "mode collapse"

## Neural Network
- **UNet** Architecture
    - Input and output of same size
    - First used for image segmentation
<p align = "center">
  <img width="458" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/32801d60-e8ac-494d-97a9-07b04a07ca3f">
</p> 

- Takes a noisy image, embeds into small space by downsampling, and upsamples to predict noise
- Can take more info. in form of _embeddings_
    - Time: related to timestep, and noise level added
    - Context: guides generation process 
 
- Checkout `forward()` in [sampling notebook](https://github.com/atul2602/How-Diffusion-Models-Work/blob/main/L1_Sampling%20.ipynb)
    
<p align = "center">
  <img width="360" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/2528e902-49dd-4d87-b480-07c5e447cc0a">
</p>

## Training
> Learns the distribution of what is "not noise"
- Sample training image, timestep `t`, and noise, randomly
    - Timestep helps control level of noise
    - randomisation ensures a stable model
- Add noise to image
- Input this into NN, which predicts the noise
- Compute loss between actual and predicted noise
- Backprop and learn
<p align = "center">
<img width="500" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/d134b4c7-fbc1-4872-b1e0-9c861cf3897a">
</p>

## Control 

- Embeddings are vectors , for instance, strings represented as number vectors
- Given as input to NN along with training image
- Get associated with a training example, and its properties
- Uses: Generate funky mixtures by combining embeddings
- Context formats
    - Text
    - Categories, one hot encoded (Eg. hero, non-hero, spells ...)   
<p align = "center">
  <img width="550" alt="image" src="https://github.com/atul2602/How-Diffusion-Models-Work/assets/61497490/38f21170-1e07-44e0-a03f-576b4250e581">
</p>

## Fast Sampling : DDIM

- DDPM is slow!
    - Multiple timesteps, and markovian nature
- Skips steps, making the process deterministic
- Lower quality than DDPM

## Summary
Other applications : Music, Inpainting, Textual Inversion


