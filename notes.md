# How Diffusion Models Work?
> Taught By Sharon Zhou 

> Noted by Atul

- Missing Prereq: [Backprop](https://www.youtube.com/watch?v=tIeHLnjs5U8)
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

