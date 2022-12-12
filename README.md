##### Table of Content

1. [Introduction](#introduction)
1. [Dataset](#dataset)
1. [References](#references)


# LandslidePTIT dataset for landslide detection problem

![](Breath-Code/figures/bilstm.png)

### Introduction
Landslides, typically a consequence of climate change and urban expansion, are one of the most common natural disasters today and cause severe troubles to human life and infrastructures all over the world. It cause roads to be blocked, which causes hurdles not only in the traffic flow but also generate various traffic problems in the form
of congestion. Therefore, there is a need to detect and warn of landslides as quickly as possible to identify proper counter-measures so that possible unfortunate consequences
can be avoided.

In our work [[1]](#1), we introduce a  landslide monitoring system that can detect quickly  whether there is any landslide occurring on roads. As one of our main contributions, we propose a data generation procedure, where the generated images are pre-processed and annotated automatically. The generated images are fuel to train a deep learning-based artificial intelligence (AI) model in the cloud layer that can rapidly detect landslides causing damages on roads.

### Dataset
The LandslidePTIT dataset was created by PTIT research team in Vietnam. It includes 2963 generated landslide images. We following the three steps (namely data crawling, data generation, and data annotation) for generating landslide images and then building a landslide dataset including generated images and their annotations.


#### DATA CRAWLING
We collect videos of road data recorded by UAV and drone, in several mountain and forest areas in Vietnam. Frames are
extracted from videos and we get a dataset consisting of 767 road images. For landslide data, we collect 149 images from the internet, with many types of slides such as rock falls, mudslides, earth flow, and depression.

#### DATA GENERATION AND AUGMENTATION
To generating data, we first need to determine the centerline of the road in road images and the landslide region in landslide images. For extracting the centerline, we adopt the pretrained
RoadNet++ model [[2]](#2) and then apply post-processing to the model output, resulting in a binary image with pixel value 1 corresponding to the centerline and 0 otherwise. For the landslide region, we crop out the region corresponding to the landslide from four types of landslide images using Labelme application ([link](https://github.com/wkentaro/labelme.git)). Finally, we randomly insert the landslide region on the centerline of the road in the image, using the Seamless Cloning algorithm [[3]](#3) method. After
conducting the data generation phase, from 767 and 149 collected road and landslide images, respectively, we obtain a generated dataset consisting of 2963 images.

After a landslide occurs, light rain is typically observed in the surrounding area. Besides, the landslides tend to occur in mountainous areas, thus the images are often captured in foggy weather. To simulate these two weather conditions, we further augment fog and rain to generate images in the LandslidePTIT dataset, which divides the dataset into three parts normal, fog, and rain.

#### DATA ANNOTATION
The images are labeled pixel-wise, i.e., each pixel of an image is annotated with a range of values from 0 to 255 that indicates the class number. For example, id 0, 1, and 2 are background, road, and earth flow, respectively. The annotations are JSON files that store coordinates of polygon forming the landslide area.

### References
<a id="1">[1]</a>
Tran-Anh, Dat and Bui-Quoc, Bao and Vu-Duc, Anh and Do, Trung-Anh and Viet, Hung Nguyen and Vu, Hoai-Nam and Tran, Cong, "Integrative Few-Shot Classification and Segmentation for Landslide Detection," in IEEE Access, vol. 10, pp. 120200-120212, 2022, doi: 10.1109/ACCESS.2022.3220906.
([link](https://ieeexplore.ieee.org/document/9943296))

<a id="2">[2]</a>
Y. Liu, J. Yao, X. Lu, M. Xia, X. Wang, and Y. Liu, “Roadnet: Learning
to comprehensively analyze road networks in complex urban scenes from
high-resolution remotely sensed images,” IEEE Transactions on Geoscience and Remote Sensing, vol. 57, no. 4, pp. 2043–2056, 2018.

<a id="3">[3]</a>
P. Pérez, M. Gangnet, and A. Blake, “Poisson image editing,” in ACM
SIGGRAPH 2003 Papers, pp. 313–318, 2003.