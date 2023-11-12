# Image Processing
We were given some images with spots. But the problem was the spots were very non-noticeable at the first glance. Our task was to do some image processing so that the spot area becomes very clear at the first glance. 

## A demo project
*It is crucial to emphasize that due to the non-disclosure agreement (NDA), I am unable to disclose the actual project or its data. The presented project is merely a demonstration, resembling the original one but featuring random images sourced from the internet.*


**Some sample images with less clear spots:**

![less clear](../Helping_Images/image_processing/less_clear.png) 
We did some heavy image processing on these images to reveal the spot area.
After doing some image processing, The corresponding images became like this:<br>
**Same images with more clear spot area:**
![more clear](../Helping_Images/image_processing/clear.png)

Some of the techniques We used are listed below:
- canny edge
- blending two images (addWeighted)
- thresholding
- different kinds of morphological transformations

We used different combinations of these techniques.


**Let's have a look at the input and output of the image processing with more details:**
![class 1](../Helping_Images/image_processing/class1.png)
![class 2](../Helping_Images/image_processing/class2.png)
![class 3](../Helping_Images/image_processing/class3.png)
![class 5](../Helping_Images/image_processing/class5.png)
![class 6](../Helping_Images/image_processing/class6.png)

### why was it important?
We used these image-processing techniques for the classification tasks also. With a small CNN, initial classification accuracy was not that high, around 80-85%. But after doing the image processing the accuracy became around 95-98% with that same small size CNN. 
