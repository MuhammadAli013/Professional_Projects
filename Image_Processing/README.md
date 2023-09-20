# Image Processing
I was given some images where there were some spots. But the problem was the spots were very non noticeable in the first glance. My task was to make some image processing so that the spot area becomes very clear in the first glance. 
*For obvious reason, I can not show the original dataset that I used for the company. I am using a similar public dataset from internet*

**some samples of images with less clear spots:**

![less clear](../Helping_Images/image_processing/less_clear.png) 
I did some heavy image processing on these images to reveal the spot area.
After doing some image processing, The corresponding images became like this:
![more clear](../Helping_Images/image_processing/clear.png)

Techniques I have used are listed below:
- canny edge
- blending two images (addWeighted)
- thresholding
- different kind of morphological transformations


![class 1](../Helping_Images/image_processing/class1.png)
![class 2](../Helping_Images/image_processing/class2.png)
![class 3](../Helping_Images/image_processing/class3.png)
![class 5](../Helping_Images/image_processing/class5.png)
![class 6](../Helping_Images/image_processing/class6.png)