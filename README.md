# **Traffic Sign Recognition** 

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./visualization/training_set_counts.png "Visualization"
[image2]: ./visualization/OriginalVs_GrayScale.png "Grayscaling"
[image3]: ./visualization/OriginalVs_GrayScaleVs_Normalize.png "Normalized"
[image4]: ./web_images/4.jpg "Traffic Sign 1"
[image5]: ./web_images/11.jpg "Traffic Sign 2"
[image6]: ./web_images/14.jpg "Traffic Sign 3"
[image7]: ./web_images/25.jpg "Traffic Sign 4"
[image8]: ./web_images/28.jpg "Traffic Sign 5"


### README

Here is a link to my [project code](https://github.com/nishantcop/CarND-Traffic-Sign-Classifier/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410 (original dataSet) + 2550 (additional images) = 6960
* The size of test set is ?
* The shape of a traffic sign image is (32,32,1)
* The number of unique classes/labels in the data set is 43

#### 2. Exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the train data is distributed per class

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

I've used the [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset) for training, validation and test purpose. 

As a first step, I decided to convert the images to grayscale because that could help reduce the training time by factor of "3".

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image2]

However, after grayscaling the validation accuracy reduced (max out on 86%). Therefore, I normalized the image that helped increase the accuracy to 98%

Here is an example of an original image, grayscale and an normalized image:

![alt text][image3]


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 GRAY image   							| 
| Convolution 3x3     	| 1x1 stride, same padding, outputs 28x28x20 	|
| RELU					|												| 
| Convolution 3x3     	| 1x1 stride, same padding, outputs 12x12x40	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x80 				    |
| Flatten       		| Output 2000						    		|
| Fully connected		| Output 120  									|
| RELU					|												|
| Fully connected		| Output 84  									|
| RELU					|												|
| Fully connected		| Output 43  									|
|						|												|
|						|												|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

EPOCHS = 20

BATCH_SIZE = 128

rate = 0.001

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:

* validation set accuracy of 99.2 
* test set accuracy of 60.0

If an iterative approach was chosen:
* I choose LeNet architcure with some basic modification to suppport GrayScale
* Accuracy was still not very good it was reaching max about 90% so I added additional Conv layer and dropout layer 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

The first image might be difficult to classify because ...

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (70km/h) 	| Speed limit (70km/h)                          | 
| Stop       			| Right-of-way at the next intersection			|
| Right-of-way at the next intersection	| Right-of-way at the next intersection	|
| Road Work	      		| Road Work			    		 				|
| Children crossing		| Keep Right           							|


The model was able to correctly guess 3 of the 5 traffic signs, which gives an accuracy of 60%. 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.0         			| Speed limit (70km/h)          				| 
| 0.0     				| Stop 										    |
| 1.0					| Right-of-way at the next intersection         |
| 1.0	      			| Road Work					 				    |
| 0.0				    | Children crossing      						|



