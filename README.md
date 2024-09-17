# Introduction
Image super-resolution aims to enhance low-resolution images into high-resolution ones, with applications ranging from medical imaging to CCTV footage. This project introduces Bilinear-SRGAN, a modified version of the SRGAN model, designed to triple the resolution of images while reducing artifacts and enhancing visual quality. The model blends bilinear interpolation with deep learning, creating a hybrid approach that improves upon traditional techniques.

# Implementation
Bilinear-SRGAN combines a bilinear interpolation layer with the SRGAN framework. The generator network includes a bilinear interpolation layer that provides an initial upscaling of the image, followed by a deep learning-based refinement process. The final output is a weighted blend of the bilinear interpolation and the SRGAN-generated image, aiming to achieve an optimal balance between initial structure and refined detail. The discriminator network ensures that the generated high-resolution images are realistic by distinguishing between real and fake images.

# Model
The model architecture consists of two main components: the generator and the discriminator. The generator is responsible for upscaling the input low-resolution images using a series of convolutional layers, batch normalization, and PReLU activation functions. Bilinear-SRGAN adapts the SRGAN model for threefold upscaling by introducing a 2D transposed convolutional layer. A bilinear interpolation layer is also incorporated to guide the initial reconstruction. The discriminator network remains similar to the original SRGAN design, serving as a feedback mechanism to improve the generator's output.

<p align="center">
  <img src="https://github.com/CandeiasV2/Bilinear-SRGAN/blob/main/Images/SRGAN%20Generator%20Diagram.png" alt="SRGAN Generator Diagram">
</p>
<p align="center">
  <em>Figure 1:  Bilinear-SRGAN model architecture composed of an adapted SRGAN model by C. Ledig et al [1] and a Bilinear model.</em>
</p>
<p align="center">
  <img src="https://github.com/CandeiasV2/Bilinear-SRGAN/blob/main/Images/SRGAN%20Discriminator%20Diagram.png" alt="SRGAN Discriminator  Diagram">
</p>
<p align="center">
  <em>Figure 2:  Discriminator model by C. Ledig et al [1].</em>
</p>

# Dataset
The model was trained using the "3x Image Super Resolution" dataset from Kaggle, consisting of 4,500 pairs of low-resolution (170x170) and high-resolution (510x510) RGB images. The dataset was split into 3,500 pairs for training and 1,000 for testing. Due to input size requirements and hardware constraints, both the low- and high-resolution images were divided into 25 equal-sized sections for processing. This preprocessing step reduced computational load, allowing the model to be trained effectively on available hardware.

# Results
Resource constraints led to a downsized version of the model, necessitating the splitting of images into 25 smaller sections. When these sections were recombined into a final high-resolution image, a visible grid-like pattern emerged, along with some color discrepancies. The model was trained on an Intel Core i7-10700K CPU, 32GB RAM, and an NVIDIA GeForce RTX 3060 Ti, with each epoch taking approximately two hours. The model was trained for 27 epochs. Although the Bilinear-SRGAN did not outperform traditional bilinear interpolation in quantitative metrics like PSNR and SSIM, it significantly enhanced the perceptual quality of images. The model produced sharper images with more intricate details compared to the baseline.

<p align="center">
  <img src="https://github.com/CandeiasV2/Bilinear-SRGAN/blob/main/Images/EE8204%20-%20Project%20Image3704.png" alt="ImageResult3704">
</p>
<p align="center">
  <em>Figure 3: Comparison of images: (a) original low-resolution image, (b) image upscaled by the Bilinear model, (c) image enhanced by the Bilinear-SRGAN model, and (d) original high-resolution image.</em>
</p>
<p align="center">
  <img src="https://github.com/CandeiasV2/Bilinear-SRGAN/blob/main/Images/EE8204%20-%20Project%20Image3503.png" alt="ImageResult3503">
</p>
<p align="center">
  <em>Figure 4: Comparison of images: (a) original low-resolution image, (b) image upscaled by the Bilinear model, (c) image enhanced by the Bilinear-SRGAN model, and (d) original high-resolution image.</em>
</p>
<p align="center">
  <img src="https://github.com/CandeiasV2/Bilinear-SRGAN/blob/main/Images/EE8204%20-%20Project%20Image3503%20Breakdown.png" alt="ImageResult3503Breakdown">
</p>
<p align="center">
  <em>Figure 5: Image processing stages with the Bilinear-SRGAN model: (a) section of the LR image, (b) result from the bilinear layer, (c) output after the final SRGAN layer, (d) final SR output, and (e) corresponding section of the HR image.</em>
</p>

# Conclusion
The Bilinear-SRGAN model introduces a novel approach to image super-resolution by incorporating a bilinear interpolation layer within the SRGAN framework. While it did not surpass the traditional bilinear model in standard evaluation metrics, it demonstrated a clear advantage in perceptual quality. Future work will focus on eliminating the grid pattern, correcting color tones, and refining the model to more accurately represent the original image quality and detail.

# Reference
[1] C. Ledig et al., “Photo-realistic single image super-resolution using a generative adversarial network,” 2017 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), Jul. 2017. [doi:10.1109/cvpr.2017.19] (https://doi.org/10.1109/cvpr.2017.19)
