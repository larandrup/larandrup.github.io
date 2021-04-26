# Multiclass Image Classifier

### Background

Classification is a systematic arrangement in groups and categories 
based on its features. Image classification came into existence for 
decreasing the gap between the computer vision and human vision 
by training the computer with the data. The image classification is 
achieved by differentiating the image into the prescribed category 
based on the content of the vision. The motivation behind this project is
to explore the study of image classification using deep learning. 
The machine learning in convolutional neural network consists of feature extraction module that extracts the important features such as edges, tex-
tures etc and a classification module that classify based on the fea-
tures extracted. The main limitation of machine learning is, while 
separating, it can only extract certain set of features on images and 
unable to  extract differentiating  features from  the training set of 
data. This disadvantage is rectified by using the deep learning. On this project, both trained convolutional neural network and transfer learning with pretrained network- ResNet50- is explored.


### Problem Statement:

Mission statement: 
To create a multiclass classifier neural network that name 
the flower type in an image and to test against a pretrained neural network. 


ResNet50 is a convolutional neural network that is 50 layers deep. Pretrained version of the network is loadable and are trained on more than a million images from the ImageNet database.

Transfer learning is using this pretrained network for fine tuning or feature extraction.


   ### Description of data
This flower dataset contains 3677 images under 5 class names and with various width and height sizes.
Downloaded from [Creative Commons](https://creativecommons.org/)


### Data Dictionary:

|Class Name|Image Count|
|--------|------|
|Sunflower|699|
|Daisy|F9|633|
|Tulip|F8|799|
|Dandelion|898|
|Rose|648|

#### Image Size
||Width|Height|
|--------|------|------|
|mean|366.05|271.99
|std|116.69|51.79|
|min|145.00|159.00|
|25%|320.00|240.00|
|50%|320.00|240.00|
|75%|500.00|333.00|
|max|1024.00|442.00|

### Data Observation 

Images in the dataset differs on:
* Varying Sizes
* Focus
* Lighting
* Shooting Angle or Photo View
* Frame Positioning
* Presence of Other Objects and/or Flowers
* Different Stages of the Flower’s life cycle
* Only a Part, Close-Ups, and Zoom-Outs 
* Color Scheme, Filters, and Black and Whites 


# Modelling
Created a base model that consists of two convolution blocks with max pool layers in each of them. Use relu as activation function for dense layer and standard output of number of classes. This model will later be tuned for high accuracy and later add ResNet50. The goal of this model is to have the highest accuracy score on classifying an unseen image as possible.

| |Base CNN|Finetuned CNN|ResNet50 with CNN|
|--------|--------|------|------|
|Accuracy Score|0.7114|0.7741 | 0.7656 | 0.9753
|Validation Accuracy Score|0.7032|0.7656|0.9272

## Data Augmentation Techniques Used:

RandomRotate, RandomCrop, RandomContrast, and RandomRotate.



 ### Conclusions
 
Five types of flowers under five classification images are sunflower, rose, tulip, dandelion, and daisy are chosen to train a convolution neural network. Data augmentation techniques played a huge part on fine tuning this neural network.

However with same dataset used for testing and validation of ResNet50 attached to a convolution neural network for classification, it is observed that the images are classified correctly at a higher accuracy rate, and misclassified understandable images. This shows the effectiveness of deep learning algorithm.

