# Road-Network-Generation-using-CGAN-from-Aerial-and-LiDAR-Images
## Overview
Deep learning techniques have shown promising results in computer vision tasks, particularly in image segmentation. 
However, most of the current deep learning approaches applied on image segmentation tasks are supervised, also fail 
to preserve spatial contiguity and cannot tackle the class imbalance issue well. Moreover, neural networks need to be 
trained on large amounts of data with high quality labels to result high accuracy. These labels are costly and difficult 
to create, hence time-consuming. To address these problems, we propose an unsupervised method that is a conditional 
generative adversarial training for the task of semantic segmentation, especially for extracting road segments in aerial images. 
In particular, we trained pix2pix based on two different generative models with the help of skip connections on satellite and LiDAR images. 
The motivation is that the proposed method can detect the roads and maintain spatial contiguity by correcting higher-order inconsistencies 
between the binary masks and the predicted images. In order to evaluate the effect of adversarial training, the proposed method is compared 
with a non-adversarial model. The results demonstrate that the generative adversarial net based on ResNet generative model gives superior 
quantitative results with an IoU score 83.1% on LiDAR data set.

![Alt text](https://drive.google.com/file/d/1Dc6GETU0toW-q70wl_140_AsXpjc3Yxe/view?usp=share_link)

## Data
The data consists of aerial and LiDAR images.  

### Aerial images -obtained from two sources:

#### 1. DoITT
Orthoimagery: The publicly available orthoimagery data of New York City is obtained from [NYC OpenData](https://opendata.cityofnewyork.us/).
Digital orthophotography for NYC has been captured on a biennial basis since 2014 during spring/summer months by [NYC Department of Information Technology and 
Telecommunication (DoITT)](https://maps.nyc.gov/tiles/). The raw aerial imagery data was corrected through computer process to remove distortions caused by elevation 
changes and camera angles by the initiative. Hence, there is no preprocessing needed. 
The image sets are available in tile format of vertical aerial imagery covering five boroughs (The Bronx, Brooklyn, Manhattan, Queens, 
and Staten Island) of New York City. 
For training, two areas of New York City are selected: Queens and Brooklyn. The reason of choosing the two biggest boroughs of NYC is to obtain various training images. 
For testing, Manhattan area is chosen. Queens, Brooklyn and Manhattan cover the area of 281.09 km2, 183.42 km2 and 59.1 km2 (https://www.census.gov), respectively.

Roadbed: The roadbed vector data of NYC is obtained from NYC OpenData provided by NYC Department of Information Technology and Telecommunication (DoITT). 
The roadbed feature class which is a layer of planimetric basemap contains the following features: roadbed - roadbed feature, intersection - intersection of roadways, 
driveway - driveway feature and shoulder -shoulder along roadway.

#### 2. Deepglobe Dataset
The satellite imagery and annotated masks used in this study derived from DeepGlobe’s road extraction challenge. The dataset is sampled from the [DigitalGlobe + Vivid Images](
https://dg-cmsuploads-production.s3.amazonaws.com/uploads/document/file/2/DGBasemapVividDS1.pdf) dataset by the initiative. The dataset covers images captured over Thailand, 
Indonesia, and India. The training data created for Road Challenge contains 6,226 satellite imagery consists of 3 channels (Red, Green and Blue), size 1, 024⇥1, 024 with 
50 cm/pixel ground resolution.

### LiDAR Images:
LiDAR discrete-return point cloud data are publicly available in the [American Society for Photogrammetry and Remote Sensing (ASPRS)](https://catalog.data.gov) in LAS (LASer)
format. 3D point cloud data, derived from Staten Island area of New York, is projected into 2D through an interpolation to local coordinate system and provided by M.Sc. Amgad Agoub 
from the Department of Geodesy and Geoinformation Science at Technical University of Berlin. The dataset contains NumPy arrays consist of null values which are only 0.01% of the whole
dataset, thus these values are simply replaced by zeros. Then, 2D arrays are converted to image representation. Created image set consists of 500 images for training and 50 images for testing. 
The final training set contains 24.5% positive and 75.5% negative pixels. and the test dataset consists of 18.2% positive and 81.8% negative pixels.

## Baseline
The baseline architecture is pix2pix (Isola et al.) which is a conditional generative adversarial network (cGAN) is adapted for the task of image segmentation. Pix2pix is relatively
different than other GAN models in terms of generator and discriminator architectures. Unlike the prior works, original pix2pix model is built upon generator network based on 
the U-Net and discriminator network based on convolutional PatchGAN architecture.  
I used both U-Net and ResNet architectures in the generator model of the pix2pix. Therefore, my generator design follows the encoder-decoder structure with skip-connections, 
as in U-Net and also ResNet, whereas the discriminator design remains the same as PatchGAN.

## Reference
Isola, P., Zhu, J. Y., Zhou, T., & Efros, A. A. (2017). Image-to-image translation with conditional adversarial networks. In Proceedings of the IEEE conference on computer vision and pattern recognition (pp. 1125- 1134).
