# 3D Object Classification and Segmentation
We did a lot of projects with 3D dataset. Most of them were related to `open3d`. Some of our tasks required 3D object classification and segmentation. Our default choice for these kind of projects were pointnet and pointnet++. 

## A demo project:
it's important to note that for NDA, I can not share actual project or actual project data. This is just a demo project similar to the original one with some random 3D objects from internet.

We did two kind of projects. 
1. Classification
2. Segmentation

*Getting a similar dataset is kind of impossible for this project. I found some dataset here: https://www.kaggle.com/datasets/priteshraj10/point-cloud-lidar-toronto-3d . This is not even close to our actual dataset. But this is all I have got without any license. The only similarities with this dataset and with my project dataset is they are both 3d point cloud with outside environment.

### Project 1: Classification
We were given some point clouds. Those point clouds were actually some chunks of a big point cloud scene. Our task was to find out if we have `object A` in that chunk. if we had `object A` in that point cloud, we considered that point cloud as our target point cloud. For this demo, Let's consider that if we have `car` in the chunk it will be considered as our target pointcloud.

#### input data:
getting a proper demo input data is very hard. 