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
Initially all images were cropped using bounding boxes from https://ai.stanford.edu/~jkrause/cars/car_dataset.html and class names were renamed accordingly. To make the model more robust some engineering adjustments were made as *Sharpening* images and applying *Gaussian Blur*. Sharpening was chosen because original images have noticable number of blur images for almost all car models, so by applying model can learn different features as well. On the other hand unseen test images might be blur especially if it is applied in real-time (moving cars) Gaussian Blur would make the model to learn features while the images look blur.

#### Training process
Training of the model is done using modified data sets which include original data, sharpened and blur images together (overall 21174 images - 19545 for train and 1629 for validation). DenseNet161 model with pretrained ImageNet weights was used as it performed the best among other architectures (https://arxiv.org/pdf/1806.02987.pdf) which achieves almost similar performance as most of the fine-grained models used so far. 




## Classification results

#### Classification results (single crop 224x224, %) on ImageNet 2012 validation set
 <table>
         <tr>
             <th rowspan="2" style="text-align:center;">Network</th>
             <th colspan="2" style="text-align:center;">Top-1 Error</th>
             <th colspan="2" style="text-align:center;">Top-5 Error</th>
             <th colspan="2" style="text-align:center;">Pre-trained models</th>
         </tr>
         <tr>
             <td style="text-align:center;">paper</td>
             <td style="text-align:center;">reproduce</td>
             <td style="text-align:center;">paper</td>
             <td style="text-align:center;">reproduce</td>
             <td style="text-align:center;">GoogleDrive</td>
             <td style="text-align:center;">BaiduCloud</td>
         </tr>
         <tr>
             <td style="text-align:center">fast MPN-COV-ResNet50</td>
             <td style="text-align:center;">22.14</td>
             <td style="text-align:center;"><b>21.71</b></td>
             <td style="text-align:center;">6.22</td>
             <td style="text-align:center;"><b>6.13</b></td>
             <td style="text-align:center;"><a href="https://drive.google.com/open?id=1h4JCWY9WfvFzNvwh2SOQwBOVVYpODuxg">217.3MB</a></td>
             <td style="text-align:center;"><a href="https://pan.baidu.com/s/17JKyy7vlWMZWGcbqcyptFg">217.3MB</a></td>
         </tr>
         <tr>
             <td style="text-align:center">fast MPN-COV-ResNet101</td>
             <td style="text-align:center;">21.21</td>
             <td style="text-align:center;"><b>20.99</b></td>
             <td style="text-align:center;">5.68</td>
             <td style="text-align:center;"><b>5.56</b></td>
             <td style="text-align:center;"><a href="https://drive.google.com/open?id=1wBAwSk51okzy-hwjrLrdNeA5bHs7YtZ0">289.9MB</a></td>
             <td style="text-align:center;"><a href="https://pan.baidu.com/s/1RbrQrrY0gEzLhkVTvdZTLQ">289.9MB</a></td>
         </tr>

</table>

#### Fine-grained classification results (top-1 accuracy rates, %)
<table>
     <tr>
         <th rowspan="2" style="text-align:center;">Backbone model</th>
         <th rowspan="2" style="text-align:center;">Dim.</th>
         <th colspan="2" style="text-align:center;"><a href="http://www.vision.caltech.edu/visipedia/CUB-200-2011.html">Birds</a></th>
         <th colspan="2" style="text-align:center;"><a href="http://ai.stanford.edu/~jkrause/cars/car_dataset.html">Aircrafts</a></th>
         <th colspan="2" style="text-align:center;"><a href="http://www.robots.ox.ac.uk/~vgg/data/oid/">Cars</a></th>
     </tr>
     <tr>
         <td> paper </td>
         <td> reproduce</td>
         <td> paper </td>
         <td> reproduce</td>
         <td> paper </td>
         <td> reproduce</td>
     </tr>
     <tr>
         <td style="text-align:center;">ResNet-50</td>
         <td style="text-align:center;">32K</td>
         <td style="text-align:center;">88.1</td>
         <td style="text-align:center;"><b>88.0</b></td>
         <td style="text-align:center;">90.0</td>
         <td style="text-align:center;"><b>90.3</b></td>
         <td style="text-align:center;">92.8</td>
         <td style="text-align:center;"><b>92.3</b></td>
     </tr>
     <tr>
         <td style="text-align:center;">ResNet-101</td>
         <td style="text-align:center;">32K</td>
         <td style="text-align:center;">88.7</td>
         <td style="text-align:center;">TODO</td>
         <td style="text-align:center;">91.4</td>
         <td style="text-align:center;">TODO</td>
         <td style="text-align:center;">93.3</td>
         <td style="text-align:center;">TODO</td>
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
│   ├── class2
│   ├── class3
│   ├── ...
│   ├── ...
│   └── classN
└── val
    ├── class1
    │   ├── class1_001.jpg
    │   ├── class1_002.jpg
    |   └── ...
    ├── class2
    ├── class3
    ├── ...
    ├── ...
    └── classN
```
*Images with 'bl' prefix show blurred, 'sh' prefix - sharpened, original images do not have any prefixes.
## Contact

**If you have any questions or suggestions, please contact me**

`orkhanh.2017@mitb.smu.edu.sg`
