# Anime face generator
![ganresults](/images/ganresults.png)

---
## Introduction
The goal for this project is to generate new images based on supplied images. In this case, I
wished to generate more anime faces based on the supplied anime face data. 

In order to do so, I used Stylegan2-ada. Stylegan2-ada is Nvidia's GAN (Generative Adversarial Network).

---
## Anime face cropper

In order to limit the scope of the image generation, we need to first crop the anime faces from the images.
While using the entire image to generate more fake images is possible, it is a lot more complicated computation
wise, and does not transfer well when using the transfer learning technique.

---
## Image preprocessor
After obtaining a set of training images, the images then need to be transformed into an appropriate data format
so that the GAN model will use. The image preprocessing step will crop the images into square images, ensure that 
the images are in the RGB colorspace, and make sure the file formats are correct.

---
## Custom docker image for GAN training
After the training data is finished with preprocessing, we need to convert it to a format that the GAN will accept. 
In the custom docker image we will use a script provided by Nvidia called ```dataset_tool.py``` that will turn the
 images into TFRecords, which can be fed into the GAN.

---
## Training on VastAI
In this step, we will then load the docker image with the TFRecords data into VastAI, which allows us to use custom
docker images on rental GPU servers. This allows us to use multiple GPUs at once, greatly decreasing the time spent
training.

After we are done training, the model can be downloaded from the results folder to produce fake images. 
Sample fake images will also be in the results folder, as well as model checkpoints and sample images at the checkpoints.

---
## Full tutorial on how to use custom images in stylegan2-ada
A text and video tutorial will be made on how to follow along in using custom images to create fake images using stylegan2-ada.
The text tutorial will be in the following pages in the Anime Face Generator directory.

* [Anime Face Cropper](/projects/animefacecrop) - Finished
* [Image Preprocessor](/projects/imagepreprocess) - In progress
* [Custom docker image for training GAN](/projects/dockerimage) - In progress
