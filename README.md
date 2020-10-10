# Super-Resolution-CNN
According to the paper, ['Image Super-Resolution Using Deep Convolutional Networks'](https://arxiv.org/pdf/1501.00092.pdf) it is possible to represent the entire process of Super-Resolution as a Deep Convolution Neural Network. This is a naive implementation of the same. This model is an `end to end` mapping between low and high-resolution images. This model takes input 64x64 image and outputs a 128x128 image.

## Dataset
Here `Linnaeus 5` dataset, which contains 6000 train images and 2000 test images, has been used. The resolution of all images is 256x256. For this model I have resized images to 64x64(which serve as the input data) and 128x128(which serve as ground truth for the respective images). 

## Model Architecture
The model architecture is similar to the model described in [Reconstructing Obfuscated Human Faces](http://cs231n.stanford.edu/reports/2017/pdfs/223.pdf).
<photo>
 
## Plots

## Results
