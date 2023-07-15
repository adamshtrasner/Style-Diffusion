# style-diffusion
This project's theme is to manipulate the style of images generated by a pre-trained denoising
diffusion model using a mechanism called classifier guidance.

This task is comprised of two main components:
* A module that computes the style loss of an image (given a style reference image). 
  The style loss computation is done by following the Neural Style-transfer algorithm by Gatys et al.
* A denoising diffusion-based image generator

The first part of the project modifies the style-transfer algorithm to perform feature inversion, text synthesis and using a different style loss.

## Feature Inversion
Modifying the neural style transfer algorithm to invert features from different stages of the
VGG-19 network, we get the following results:
![Feature Inversion](images/feature_inversion.jpg)

We can see that as we go deeper and deeper in the layers, it is
harder to reconstruct the exact features of the image, and the colors
and texture of the reconstruction of images from deeper layers are
different than the original image. This aligns with the logic of feature
inversion: deeper layers tend to have larger receptive fields, which
means they capture more global features. The feature maps at
deeper layers contain less specific information about the exact
arrangement of pixels in the original image. Moreover, deeper layers
of the VGG-19 model consist of more complex features that capture
high-level representations. So, when performing feature inversion, it
becomes challenging to precisely reconstruct these complex
features from noisy initial images.

## Texture Synthesis
Modifying the neural style transfer algorithm to generate a texture inspired by the style
input, we get the following results:
![Texture Synthesis](images/style_synthesis.jpg)

Here we see that the deeper the layers, the more we capture more of
the style of the original styled image and we get a nice texture and
patterns. This aligns with the texture synthesis logic, since the early
layers capture low-level features such as edges and simple textures,
while the deeper layers capture higher-level features such as
complex textures, object parts, etc.
