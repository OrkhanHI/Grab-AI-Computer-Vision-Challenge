## Grab AI Computer Vision Challenge on publicly available "Cars" dataset

DenseNet architecture
<div>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;<img src="images/DenseNet.png" width="80%"/>
</div>

*DenseNet161 architecture was used as a backbone for this project.*
## Introduction

This repository contains the code in Jypyter Notebook with **PyTorch** framework pretrained on ImageNet dataset and includes:

<b>For Training:</b>
- *Preprocess-Train_Valid.ipynb*
- *To_SHARPEN_train_images.ipynb*
- *Train.ipynb*<br>

<b>For Testing:</b>
- *Preprocess-Test.ipynb*
- *Test.ipynb*



#### Preprocessing (Feature Engineering)
1.Two files from Stanford repository *cars_train.tgz* and *car_devkit.tgz* need to be uploaded from repository website. After running *Preprocess-Train_Valid.ipynb* <b>data folder</b> will be created with *train* and *valid* folders respectively with their respective bounding boxes and class names.
<br>
2.To make the model more robust some engineering adjustments were made such as *Sharpening* images by running *To_SHARPEN_train_images.ipynb*. Sharpening was chosen as original images have noticable number of blur images for almost all car models, so by applying sharpening the model can learn features better.
<br>
3.To create the test folder *cars_test.tgz* need to be uploaded from repository website and *Preprocess-Test.ipynb* need to be run which will create inside the data folder *test* images folder.
<br><br>

#### Training process
*Train.ipynb* inside the code folder was used to train the model.
Training of the model is done using modified data sets which include original and sharpened data with 80/20 partition (overall 14659 images - 13030 for train and 1629 for validation which does not include sharpened data). DenseNet161 model with pretrained ImageNet weights was used as it performed the best among other architectures (https://arxiv.org/pdf/1806.02987.pdf) which achieves almost similar performance as most of the fine-grained models used so far. 



## Classification results

 <table style="width:100%">
         <tr>
             <th rowspan="2" style="text-align:center;">Network</th>
             <th colspan="2" style="text-align:center;">Top-1 Accuracy</th>
             <th colspan="2" style="text-align:center;">Top-5 Accuracy</th>
             <th rowspan="2" style="text-align:center;">Pre-trained model</th>
         </tr>
         <tr>
             <td style="text-align:center;">Val</td>
             <td style="text-align:center;">Test</td>
             <td style="text-align:center;">Val</td>
             <td style="text-align:center;">Test</td>
         </tr>
         <tr>
             <td style="text-align:center">DenseNet161</td>
             <td style="text-align:center;">90.67</td>
             <td style="text-align:center;"><b>90.24</b></td>
             <td style="text-align:center;">98.47</td>
             <td style="text-align:center;"><b>98.43</b></td>
             <td style="text-align:center;">ImageNet</td>
         </td>
</table>


- The code was totally created from scratch without any reference to above mentioned paper code.
- Different dataset was created in order to increase the accuracy. Sharpening the data which was my own approach indeed made the model more robust.
- The results are obtained by comparing different optimizers and learning rates, which were not described in the paper in details. *Adagrad* optimizer performed the best among others with 0.001 *learning rate*.
- Many other fine-grained models were used, however, most of the paper results are impossible to reproduce. I have also tried "Towards Faster Training of Global Covariance Pooling Networks by Iterative Matrix Square Root Normalization" (https://arxiv.org/pdf/1712.01034.pdf), but the model took longer training time with relatively lower accuracy (less than 90%).

## Installation and Usage

1. Pytorch 1.0.1 was used
2. type `git clone https://github.com/OrkhanHI/Grab-AI-Computer-Vision-Challenge.git`
3. `pip install -r requirements.txt`
4. prepare the dataset as follows
```
.
├── train
│   ├── 0001 AM General Hummer SUV 2000
│   │   ├── 1sh_00163.jpg
│   │   ├── 1sh_00462.jpg
|   |   └── ...
│   ├── 0002 Acura RL Sedan 2012
│   ├── 0003 Acura TL Sedan 2012
│   ├── ...
│   ├── ...
│   └── 0196 smart fortwo Convertible 2012
└── valid
    ├── 0001 AM General Hummer SUV 2000
    │   ├── 01277.jpg
    │   ├── 01952.jpg
    |   └── ...
    ├── 0002 Acura RL Sedan 2012
    ├── 0003 Acura TL Sedan 2012
    ├── ...
    ├── ...
    └── 0196 smart fortwo Convertible 2012
```
5. Download best_model_weights from https://drive.google.com/file/d/1vkwNVqTS3ikBNzq4Atz3S7ylBpiTZgX6/view?usp=sharing and copy to *outputs* folder above (because size of the weights is big please use link to download and copy to the output folder) which will be used in *test.ipynb*.
6. For Test case preprocess data using Preprocess-Test.ipynb <br>
*<b>Note:*</b> Only train images were augmented with sharpen preprocessing.
Images with 'sh' prefix mean sharpened, original images do not have any prefixes.
## References
Krassimir Valev, Arne Schumann, Lars Sommer, and Jurgen Beyerer,"A Systematic Evaluation of Recent Deep Learning Architectures for Fine-Grained Vehicle Classification", arXiv:1806.02987v1 [cs.CV] 8 Jun 2018

## Contact

**If you have any questions or suggestions, please contact me**

`orkhanh.2017@mitb.smu.edu.sg`
