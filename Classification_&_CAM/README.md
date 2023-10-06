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
Another data preparation step is Image processing. As I mentioned earlier, most of our NG dataset's spot is indistinguishable. In some cases, it's very difficult to identify at the first glances. In those cases if we do some kind of image processing, the spot becomes very distinguishable. Let's have a look the result of some image processing:

Good Case:
![good case](../Helping_Images/image_classification/good_case.png)

Bad Case:
![bad case](../Helping_Images/image_classification/bad_case.png)

From above two images it's very clear that after image processing, The spot is very distinguishable now. 
For most of the cases this types of image processing actually helped us a lot for image classification problem. 
**You will find some of my image processing tasks here in the[Image_Processing folder](../Image_Processing/)**.


#### Training
- Most of the time we used `transfer learning` for training purposes. We used vgg, resnet, mobilenet, inception,xception etc models. 
- However, industry data were very different than `imagenet` dataset. So we had to `unfreeze` some of the last layers to let the model be trained. How many layers to be unfrozen or how many layers to be added actually depends heavily on the dataset.
- if the dataset is similar to `imagenet` a few unfrozen layers are okay. But if the dataset is very different than `imagenet`, number of unfrozen layers must be increased. 

This is a simple training dataflow:
![training](../Helping_Images/image_classification/training.png)

- Depending on the dataset, Our accuracy varied a lot. For this particular dataset accuracy varies around `99%`. The reason is very simple. After image processing, it is a very easy dataset. 
- However, For a lot of cases, Accuracy were not our main goal. F1-score, recall, precision etc were even more important than accuracy depending on the dataset. 

#### Inference
Inference of this project is very straight forward. Just we had to keep in mind one thing: *what was our preprocessing?*. If we do the same preprocessing that we did in training, the inference is good to go. 

## Class Activation Map (CAM)
Sometimes 