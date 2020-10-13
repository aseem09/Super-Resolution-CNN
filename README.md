# Super-Resolution-CNN
It is possible to represent the entire process of Super-Resolution as a Deep Convolution Neural Network. The start-of-the-art model for Super-resolution is based on GANs. This repository contains the CNN-based implementaion which is an end to end mapping between low and high-resolution images. It takes as input a 64x64 image and outputs a 128x128 image.

## Dataset
Here `Linnaeus 5` dataset, which contains 6000 train images and 2000 test images, has been used. The resolution of all images is 256x256. For this model I have resized images to 64x64(which serve as the input data) and 128x128(which serve as ground truth for the respective images). 

## Model Architecture
The CNN architecture is similar to one described in ['Reconstructing Obfuscated Human Faces'](http://cs231n.stanford.edu/reports/2017/pdfs/223.pdf).

Click [here](https://user-images.githubusercontent.com/43964071/95691772-509ef600-0c3f-11eb-86f8-f1639ead7288.png) to view the model architecture.

## Loss Function
In the un-optimized version `MeanSquaredError` is used as loss function. This resembles with the Pixel Loss which is given as-

<img src="https://user-images.githubusercontent.com/43964071/95792300-d767d780-0d00-11eb-9c98-1f63991976f3.png">

In the optimized version a linear combination of Pixel Loss and Perceptual Loss is used. Perceptual loss gives an estimate of difference between feature map of image between this model and, say, a pre-trained VGGNet. The Perceptual loss is given as-

<img src="https://user-images.githubusercontent.com/43964071/95792298-d636aa80-0d00-11eb-92df-87aff73b1bd8.png">
Here Φ denotes the activation of the 6th layer of a pre-trained VGGNet16 model. 

To view the architecture of custom VGG model click [here](https://user-images.githubusercontent.com/43964071/95691772-509ef600-0c3f-11eb-86f8-f1639ead7288.png)

The final loss function looks something like-

<img src="https://user-images.githubusercontent.com/43964071/95794282-2152bc80-0d05-11eb-985e-bf192ecd26d2.png"> 

Where,
<img src="https://user-images.githubusercontent.com/43964071/95794345-4810f300-0d05-11eb-8fa3-f333ef1454ca.png">


## Results
### 1. Un-Optimized Model

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95691989-1c2c3980-0c41-11eb-8ffe-c26277e89b35.jpg" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95692407-294a2800-0c43-11eb-9dba-e80fb4250645.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95691988-1afb0c80-0c41-11eb-854f-0873fbe5d76d.jpg" width="220px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95692521-fb191800-0c43-11eb-8789-3433a6d6d2b5.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95691995-22bab100-0c41-11eb-939d-6f9818d83f07.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95691993-21898400-0c41-11eb-8fd1-0726351cbb72.jpg" width="220px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95691997-23ebde00-0c41-11eb-84b5-1864dc419317.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95691999-251d0b00-0c41-11eb-9db2-509b64b6c351.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95691996-23534780-0c41-11eb-9fb2-6de5635eeee9.png" width="220px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95692463-98c01780-0c43-11eb-8a00-03121636f231.png" width="220px" border="1px"> | <img src="https://user-images.githubusercontent.com/43964071/95692464-9958ae00-0c43-11eb-933c-1300077d478e.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95692462-978eea80-0c43-11eb-853b-32156425a976.png" width="220px">

These images quite clearly show that model performs pretty well with it comes to smoothening out curves and edges. 
However, it can be seen that the images are blurry and miss intricate details. The can be resolved by adding the `Perceptual Loss` to the `Pixel Loss` function.  This forces the model to focus more on detailed structures of the objects in the image.

### 2. Optimized Model

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95793487-5100c500-0d03-11eb-9c1a-1c36175ff5ff.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793490-51995b80-0d03-11eb-9fe9-c4402cfd30fb.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793485-4fcf9800-0d03-11eb-88bd-bff705570297.png" width="220px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95793496-52ca8880-0d03-11eb-95f5-e3b5ff79635b.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793497-53631f00-0d03-11eb-819c-6da6f7bb5359.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793494-5231f200-0d03-11eb-98e2-57dd689bc96e.png" width="220px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95793771-f3b94380-0d03-11eb-94f3-fe08f6d3621b.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793772-f3b94380-0d03-11eb-80f9-7008fe0cb78e.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793770-f2881680-0d03-11eb-9a5e-4902ce92391a.png" width="220px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95793513-58c06980-0d03-11eb-922f-05250820593d.png" width="220px" border="1px"> | <img src="https://user-images.githubusercontent.com/43964071/95793514-59590000-0d03-11eb-9795-eedd33987e55.png" width="220px"> | <img src="https://user-images.githubusercontent.com/43964071/95793510-5827d300-0d03-11eb-83fb-b59ef986741d.png" width="220px">

After taking into consideration the Perceptual Loss the model performs way better. Though there is one drawback. The images have a checkerboard like pattern in which is solely due to the perceptual loss. This model also gives a value of around 35-36db for a few images when PSNR(Peak Signal to Noise Ratio) is calculated.

