# Image Detection
Similar to image segmentation, we did a lot of projects related to image detection. As a member of the AI research team, I was a part of those projects. For some cases, I did a portion of the projects, for other cases I did the whole thing. Here, I will show you a demo project about image Detection. I did similar projects related to image detection.

## A demo Project

*It is crucial to emphasize that due to the non-disclosure agreement (NDA), I am unable to disclose the actual project or its data. The presented project is merely a demonstration, resembling the original one but featuring random images sourced from the internet*

#### introduction
Say, we were given some big orthoimages or big drone images. Those images contained Banana fields and some other parts. Our target object is faulty banana trees. So every other thing was just background. Banana tree had 3 classes: `class_1`, `class_2`, and `class_3`. 
- `class_1` means a little yellowish green tree. Nothing to worry about.
- `class_2` means the tree is already very yellow. Measures should be taken.
- `class_3` means the tree is dying. The color is yellow to brown. We need to get rid of it. 

**Most of the trees were completely green. They were not our target object. So they were also considered as background**

The ultimate target of that project was to find out which banana tree should be investigated and to get an overall idea over a huge amount of land.

#### Input dataset and annotation:
We were given big orthoimages ( or big drone JPEG images in some cases ). The demo images and annotation of the images were like this.

Say, this is the input image:
![input image](../Helping_Images/detection/input_image.png)

- This is an aerial image
- The image is taken from a 90 degree angle

First, we did the annotation. We identified the banana trees from the above-mentioned classes. If it did not belong to those classes it was considered as the Background.
![annotation](../Helping_Images/detection/annotation.png)
in this demo case: the green box indicates class_1, the orange box indicates class_2 and the red box indicates class_3.

#### Processing:
For annotation purposes, it was easy to use drone images or orthoimages. But to train the model we needed to convert both the images and the annotations into reasonable sizes. Say, We chose 1024x1024. These tiles ( images and the annotations) were fed to train the detection model. Here you can see the tiles in black boxes.
![tiling](../Helping_Images/detection/tiling.png)

For every tile, we had to create an annotation `.txt` file. Say in a tile there are two of our target objects. In that case, the `.txt` file related to the image will have 2 lines. It will be something like this:
```
2 235 512 80 200
0 400 335 100 120
```
**Explanations:**
- `2 235 512 80 200`: 
    - `2` indicates the class. `2` means it's from class_3 (very bad)
    - `235` means X_center of the bounding box
    - `512` means Y_center of the bounding box
    - `80` means W of the bounding box
    - `200` height of the bounding box
- `0 400 335 100 120`:
    - `0` indicates the class. `0` means it's from class_1 (nothing to worry about)
    - `400` means X_center of the bounding box
    - `335` means Y_center of the bounding box
    - `100` means W of the bounding box
    - `120` height of the bounding box

If a tile has only one target object it will have only one line in the related `.txt` file. If it has no target object, the related `.txt` file will be empty.

We set up the dataset like this:
```
custom_dataset/
├── data/
│   ├── obj.names
│   ├── obj.data
├── cfg/
│   ├── yolov3.cfg
├── train.txt
├── valid.txt
└── images/
    ├── image1.jpg
    ├── image2.jpg
    └── ...
```
- obj.names: A text file containing one class name per line (e.g., "class_1," "class_2", "class_3").
- obj.data: A configuration file containing dataset information, including the paths to obj.names, train.txt, valid.txt, and the number of classes.
- yolov3.cfg: The YOLOv3 configuration file we'll modify (more on this below).
- train.txt and valid.txt: Text files listing the paths to our training and validation images (one path per line).
- images/: A folder containing our labeled training images.

We also had to modify our config file (`cfg/yolov3.cfg` file) to meet the criteria of our dataset. We used a pretrained model from the darknet repository. Training a huge yolov3 model from scratch was not a viable option for us. Because we had a limited number of images and as always it would have taken a lot of time to train a yolov3 from scratch.

#### Training
Training a yolov3 model is pretty straightforward. As we used darknet repo, they have specific command line info to run a yolov3 model.
the command is something like this:
```
./darknet detector train data/obj.data cfg/yolov3.cfg darknet53.conv.74
```

#### Inference
This part is tricky actually. As we can not use a big image for training same goes for inference. Say a drone image is 5000x4000 pixels. It's not possible to use this whole image. So we had to cut the images into tiles, and then merge the tiles to rebuild the full prediction of the image.

Consider it as a test image of a bigger size. So we have to make tiles to use with the model:
![inference 1](../Helping_Images/detection/inference_1.png)

The tiles from the test image:
![inference 2](../Helping_Images/detection/inference_2.png)

The output from the model for each tile:
![inference 3](../Helping_Images/detection/inference_3.png)

This is not fully true. We actually got `class, X_center, Y_center, W, H`` values for every object from an input tile. The above image is actually a visualization using those values.

This is the inference summary:

![inference 4](../Helping_Images/detection/inference_4.png)

#### If geo-information is available in the test photo
In test images, if we have an orthophoto with geo information, we could do the prediction with that geo-information after merging the tiles. We could then see the exact location of the dataset and the prediction in the map with appropriate applications (ex: QGIS). So our customers could go to those specific map locations to handle the issues with the banana trees.

#### why YOLOv3
when we did the project the available options were YOLOv3 and YOLOv4. We used YOLOv3 because it gave us better results for our dataset compared to YOLOv4.
