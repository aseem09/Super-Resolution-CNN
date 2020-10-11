# Super-Resolution-CNN
According to the paper, ['Image Super-Resolution Using Deep Convolutional Networks'](https://arxiv.org/pdf/1501.00092.pdf) it is possible to represent the entire process of Super-Resolution as a Deep Convolution Neural Network. This is a naive implementation of the same. This model is an end to end mapping between low and high-resolution images. This model takes input 64x64 image and outputs a 128x128 image.

## Dataset
Here `Linnaeus 5` dataset, which contains 6000 train images and 2000 test images, has been used. The resolution of all images is 256x256. For this model I have resized images to 64x64(which serve as the input data) and 128x128(which serve as ground truth for the respective images). 

## Model Architecture
The CNN architecture is similar to one described in ['Reconstructing Obfuscated Human Faces'](http://cs231n.stanford.edu/reports/2017/pdfs/223.pdf).

Click [here](https://user-images.githubusercontent.com/43964071/95691772-509ef600-0c3f-11eb-86f8-f1639ead7288.png) to view the model architecture.

## Loss Function
For super-resolution Pixel Loss Function is quite effective. A similar loss function `MeanSquaredError` has been used here. For tasks like super-resolution and neural net style transfer, usually Perceptual Loss function is also taken into account.

## Results
The model was trained for a few epochs and the following results were observed.

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95691989-1c2c3980-0c41-11eb-8ffe-c26277e89b35.jpg" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95692407-294a2800-0c43-11eb-9dba-e80fb4250645.png" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95691988-1afb0c80-0c41-11eb-854f-0873fbe5d76d.jpg" width="200px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95692521-fb191800-0c43-11eb-8789-3433a6d6d2b5.png" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95691995-22bab100-0c41-11eb-939d-6f9818d83f07.png" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95691993-21898400-0c41-11eb-8fd1-0726351cbb72.jpg" width="200px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95691997-23ebde00-0c41-11eb-84b5-1864dc419317.png" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95691999-251d0b00-0c41-11eb-9db2-509b64b6c351.png" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95691996-23534780-0c41-11eb-9fb2-6de5635eeee9.png" width="200px">

Input(64x64)               |  Ground Truth             | Predicted
:-------------------------:|:-------------------------:|:-------------------------:
 <img src="https://user-images.githubusercontent.com/43964071/95692463-98c01780-0c43-11eb-8a00-03121636f231.png" width="200px" border="1px"> | <img src="https://user-images.githubusercontent.com/43964071/95692464-9958ae00-0c43-11eb-933c-1300077d478e.png" width="200px"> | <img src="https://user-images.githubusercontent.com/43964071/95692462-978eea80-0c43-11eb-853b-32156425a976.png" width="200px">

These images quite clearly show that model performs pretty well with it comes to smoothening out curves and edges. 
However, it can be seen that the images are blurry and miss intricate details. The can be resolved by adding the `Perceptual Loss` to the `Pixel Loss` function. Perceptual loss gives an estimate of difference between feature map of image between this model and, say, a pre-trained VGGNet. This forces the model to focus more on detailed structures of the objects in the image.
