## Grab AI Computer Vision Challenge on publicly available "Cars" dataset

DenseNet architecture
<div>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;<img src="images/DenseNet.png" width="80%"/>
</div>

*DenseNet161 architecture was used as a backbone for this project.*
## Introduction

This repository contains the code in Jypyter Notebook with **PyTorch** framework pretrained on ImageNet dataset and includes:

- *Preprocessing.ipynb*
- *Train.ipynb*
- *Test.ipynb*

#### Preprocessing (Feature Engineering)
Initially all images were cropped using bounding boxes from https://ai.stanford.edu/~jkrause/cars/car_dataset.html and class names were renamed accordingly.<br><br>
*Preprocess-Train_Valid.ipynb* was used to upload the images from above link and put the bounding boxes and respective class names.
<br><b>In order to upload test unseen images *Preprocess-Test.ipynb file need to be run* which will create Test folder with images and bounding boxes provided from Stanford web-page will be applied.</b><br>
To make the model more robust some engineering adjustments were made as *Sharpening* images and applying *Gaussian Blur*. Sharpening was chosen because original images have noticable number of blur images for almost all car models, so by applying model can learn different features as well. On the other hand unseen test images might be blur especially if it is applied in real-time (moving cars) Gaussian Blur would make the model to learn features while the images look blur.

#### Training process
Training of the model is done using modified data sets which include original data, sharpened and blur images together (overall 21174 images - 19545 for train and 1629 for validation). DenseNet161 model with pretrained ImageNet weights was used as it performed the best among other architectures (https://arxiv.org/pdf/1806.02987.pdf) which achieves almost similar performance as most of the fine-grained models used so far. 



## Classification results

#### Classification results (single crop 224x224, %) on ImageNet 2012 validation set


<table style="width:100%">
  <caption><b>Classification Results</b></caption>
  <tr>
    <th>Network</th>
    <th>Top-1 Accuracy</th>
    <th>Top-5 Accuracy</th>
    <th>Pre-trained models</th>
  </tr>
  <tr>
    <td style="text-align:center"><b>DenseNet161</b></td>
    <td style="text-align:center">1111</td style="text-align:center">
    <td style="text-align:center">2222</td>
    <td style="text-align:center">ImageNet</td>
  </tr>
</table>

- The code was totally created from scratch by me without any reference to above mentioned paper code.
- Different dataset was created in order to increase the accuracy.
- The results are obtained by simply comparing different optimizers and learning rates, which were not described in the paper in details. *Adagrad* optimizer performed the best among others with 0.001 *learning rate*.


## Installation and Usage

1. Pytorch 1.0.1 was used
2. type `git clone https://github.com/jiangtaoxie/fast-MPN-COV`
3. `pip install -r requirements.txt`
4. prepare the dataset as follows
```
.
├── train
│   ├── 0001 AM General Hummer SUV 2000
│   │   ├── 1bl_00163.jpg
│   │   ├── 1sh_00163.jpg
|   |   └── ...
│   ├── 0002 Acura RL Sedan 2012
│   ├── 0003 Acura TL Sedan 2012
│   ├── ...
│   ├── ...
│   └── 0196 smart fortwo Convertible 2012
└── valid
    ├── 0001 AM General Hummer SUV 2000
    │   ├── 00946.jpg
    │   ├── 01918.jpg
    |   └── ...
    ├── 0002 Acura RL Sedan 2012
    ├── 0003 Acura TL Sedan 2012
    ├── ...
    ├── ...
    └── 0196 smart fortwo Convertible 2012
```
*Only train images were augmented with sharpen and blur preprocessings*.<br>
Images with 'bl' prefix show blurred, 'sh' prefix - sharpened, original images do not have any prefixes.
## Contact

**If you have any questions or suggestions, please contact me**

`orkhanh.2017@mitb.smu.edu.sg`
