# SwinIR_project

This project is a re-implementation of the work of Jingyun Liang, Jiezhang Cao, Guolei Sun, Kai Zhang, Luc Van Gool and Radu Timofte. The official PyTorch implementation of SwinIR: Image Restoration Using Shifted Window Transformer is available here: https://github.com/JingyunLiang/SwinIR and https://github.com/cszn/KAIR.git

The entire work is based on the following arXiv paper: https://arxiv.org/abs/2108.10257v1

############################################################################################

########################################### INTRODUCTION ####################################

############################################################################################
    

Image restoration is a long-standing low-level vision problem that aims to restore high-quality images from low-quality images (e.g., downscaled, noisy and compressed images).

In this paper it was proposed a strong baseline model SwinIR for image restoration based on the Swin Transformer. SwinIR is characterized by three parts: shallow feature extraction, deep feature extraction and high-quality image reconstruction. The deep feature extraction module is composed of several residual Swin Transformer blocks (RSTB), each of which has several Swin Transformer layers together with a residual connection.

The experiments were done over different tasks:

    image super-resolution classical
    image super-resolution lightweight
    image super-resolution real-world
    grayscale image denoising
    color image denoising
    JPEG compression artifact reduction

![immagine](https://user-images.githubusercontent.com/73338494/202896611-596c9a1a-7ca0-4667-b881-e2a91caa477d.png)

############################################################################################

########################################### MODEL ####################################

############################################################################################


![immagine](https://user-images.githubusercontent.com/73338494/202896751-c2b29031-b3d0-4f00-b632-e451ad99da9a.png)


SwinIR is characterized by three parts: shallow feature extraction, deep feature extraction and high-quality image reconstruction.

Shallow and deep feature extraction
![immagine](https://user-images.githubusercontent.com/73338494/202896982-eb5bde3d-1232-434a-88b4-88091cd506ec.png)


Image reconstruction
![immagine](https://user-images.githubusercontent.com/73338494/202896998-93c08735-e115-40d7-b5f6-aeb001d04ee9.png)


Loss function
![immagine](https://user-images.githubusercontent.com/73338494/202897012-7e427804-f7e3-4161-9820-40f31faa096b.png)




############################################################################################

########################################### METRICS ####################################

############################################################################################

Peak signal-to-noise ratio (PSNR) is the ratio between the maximum possible power of a signal and the power of corrupting noise that affects the fidelity of its representation.
![immagine](https://user-images.githubusercontent.com/73338494/202896885-1795bec3-1324-4967-89d5-2cce0c52bc62.png)

![immagine](https://user-images.githubusercontent.com/73338494/202896891-05f1dae4-bba7-443b-b481-1e315d858878.png)

MAXI is the maximum possible pixel value of the image. When samples are represented using linear PCM with B bits per sample, MAXI is 2B − 1.

The structural similarity index measure (SSIM) is a method for predicting the perceived quality of digital images. It is a decimal value between 0 and 1


############################################################################################

########################################### RESULTS ####################################

############################################################################################



![immagine](https://user-images.githubusercontent.com/73338494/202897116-04a2999c-1f1c-4e26-9eb5-993ea0231489.png)

![immagine](https://user-images.githubusercontent.com/73338494/202897171-29f8790b-73bd-4e35-91c9-4201eddd7454.png)

![immagine](https://user-images.githubusercontent.com/73338494/202897176-04c4d440-f665-40e9-920c-1831ef48574c.png)


In Classical Image SR I trained SwinIR both on DIV2K and DIV2K+Flickr2K dataset and tested it on Set5 and Set14 dataset respectively. The maximum PSNR gain reaches 38.35 dB on Set5 for scale factor 2 and the best SSIM reaches 0.9620, so it is highly reliable. As you can see from the results, SwinIR can restore high-frequency details and alleviate the blurring artifacts, resulting in sharp and natural edges. The same is applied on Lightweight Image SR. The difference between the two tasks is in the embedding dimension (180/60), in image size (48/64) and type of up sampler (pixelshuffle/pixelshuffledirect).

![immagine](https://user-images.githubusercontent.com/73338494/202897186-4802c0ab-d804-4758-86ae-d5cb24f3c500.png)

![immagine](https://user-images.githubusercontent.com/73338494/202897195-dc18266b-853e-4938-83e6-8e98c33b5cf5.png)

![immagine](https://user-images.githubusercontent.com/73338494/202897203-a734ab7f-b5c4-4ba6-ba03-7e8ea9a8c452.png)

In Real-World Image SR I trained SwinIR both on DIV2K+Flickr2K+OST and DIV2K+Flickr2K+OST+FFHQ+Manga109+SCUT dataset and tested it on RealSRSet+5images dataset. This task works perfectly for real-world scenarios, even small details and imperfections are perfectly reconstructed. 


![immagine](https://user-images.githubusercontent.com/73338494/202897230-b1ca31fc-6da0-46d9-b4cc-980750494ff4.png)

![immagine](https://user-images.githubusercontent.com/73338494/202897240-807bb1bb-9610-45d8-b487-2b73d221c37a.png)

Since there is no ground-truth high-quality images, I only provide visual comparison with representative bicubic model ESRGAN and state-of-the-art real world image SR models RealSR, BSRGAN and Real-ESRGAN. SwinIR produces visually pleasing images with clear and sharp edges, whereas other compared methods may suffer from unsatisfactory artifacts.

![immagine](https://user-images.githubusercontent.com/73338494/202897258-d0f1f15b-ff7e-4dce-9d6f-e524ad7ac6b9.png)

![immagine](https://user-images.githubusercontent.com/73338494/202897267-1b382429-fd03-4209-9b3a-c099a9cc7b97.png)

In Image Denoising I trained SwinIR on DIV2K+Flickr2K+BSD500 dataset and tested it on Set 12 (gray) and McMaster (color) dataset. The maximum PSNR gain reaches 38.42 dB on McMaster for noise factor 15 and the best SSIM reaches 0.9598, so it is reliable. 
As you can see, our method can remove heavy noise corruption and preserve high-frequency image details, resulting in sharper edges and more natural textures. Irrelevant details like the stripes of the girl’s hat, the shadows and the tower in background are completely removed.



*********************************************************************************************
*****AUTHOR----------> Leonardo Mongelli -----> mongelli.2020024@studenti.uniroma1.it  ******
*********************************************************************************************
