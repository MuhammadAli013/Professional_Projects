# Classification and Class Activation Mapping (CAM)
We did a lot of image classification project. Mainly the target objects were industry items. We did both binary classification and multi class classification. But most of our classification tasks were binary classification detecting 
1.  Good condition objects (OK) and
2.  Not Good condition objects (NG) . 
Here I will show a similar demo projects about binary image classification.

## A Demo Project
it's important to note that for NDA, I can not share actual project or actual project data. This is just a demo project similar to the original one with some random images from the internet.

#### introduction
Say we were given 2 types of images. Some of them are good images (OK) and some of them are bad images (NG). We have to identify which one is which. Let's have a look at 2 images from our demo dataset:

![good bad unclear](../Helping_Images/image_classification/good_bad_unclear.png)

There is a spot in the bad case. But as you can see, the spot is not very distinguishable. To make it clear I am making a red circle around the bad case point.
![bad case](../Helping_Images/image_classification/badcase.png)

Most of our dataset were like this or even harder to find out the bad spot. Our classification model had to face two problems:

1. bad case spot is very undistinguishable in many cases. 
2. Number of good cases examples were too high compared to number of bad case examples.

We solved these two problems. And I will explain them here also.

#### Data preparation:
##### Handling data imbalance
For most of the cases we had a huge class imbalance. There were lot's of Good cases and less number of Bad cases. So we had to a lot of augmentation. 
- The common augmentation that we used are: horizontal flipping, vertical flipping, rotation, translation, cropping, color jittering ( brightness, contrast), deformation etc.
- We augmented both good cases and bad cases. We took samples from good cases and bad cases. Say we took 500 samples from augmented good cases and 500 samples from augmented bad cases. So now there is no data imbalance.
- Sometimes number of bad cases are two low and augmentation is not a viable options. In those cases we had to change the `loss function`. we had to put more weights in minority class to give it more importance.

##### Image processing
