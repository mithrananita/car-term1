# **Traffic Sign Recognition - Mithran Mathew** 


---

**Build a Traffic Sign Recognition Project**

Please use my jupyter notebook for a full writeup with code and explanation

https://github.com/mithrananita/car-term1/blob/master/Project2/Project2_Sign_Classifier.ipynb

This project is to take German traffic sign data, loaded as 32x32 color images, and classify them properly. Data provided as input is
* training dataset (35k images)
* Validation dataset (4k images)
* and Test dataset (12.6k images)

The task is to train and repeatedly test on the validation dataset, but try on the test dataset only once.This python notebook will attempt to go through each step

1. setting up loading
2. Visualizing the data
3. normalizing images
4. setting up the convolutional neural network,
5. calculating a cost function and validation accuracy (using adams optimizer)

And running over multiple EPOCHS and batches till adjust weights converge to 1 (or as close as possible)
I will then attempt to train new traffic images loaded off the web with this classifier once this is done.

### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/mithrananita/car-term1/blob/master/Project2/Project2_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x1
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

See Output [5] in the Jupyter Notebook

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because for sign recognition color is less important than luminance/contrast and shapes

I did a simple conversion to Luminance using the following function
https://en.wikipedia.org/wiki/YIQ

I then converted to a simple normalized value using the (pixel - 128)/ 128  function

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Greyscale image normalized between -0.5 and 0.5 (0 mean)   							| 
| Convolution 5x5     	| 1x1 stride, same padding, outputs 28x28x6 	|
| RELU					|				Rectified Linear Function								|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	   | stride 1x1 14x14x6 input output 10x10x6     									|
| RELU					|				Rectified Linear Function								|
| Max pooling	      	| 2x2 stride,  outputs 5x5x6 				|
| Fully connected		| 120 outputs .        									|
| RELU					|				Rectified Linear Function								|
| Fully connected		  | 84 outputs .        									|
| Logits		      | Fully Connected 84 inputs converted to 43 outputs    									|

 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train my model, I used a 
* batch size of 128, 
* an EPOCH size of 50, 
* a learning parameter of .0001

I tried to lower and raise the learning parameter, this had some poor results in terms of accuracy, likely underfitting the space
.
I tried to lower the EPOCH size, some times this was good, it was not converging to above 93% consistently

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 1
* validation set accuracy of .954 
* test set accuracy of .92

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen? 
  I tried to mistakenly use 10 outputs, the results were not converging!
* What were some problems with the initial architecture?
  I started with the LeNet architecture, there really wasn't that much tweaking I needed to do to get to 93% validation accuracy
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
  I didn't see much effect from anything other than changing the EPOCHs, this helped get above 95% accuracy
* Which parameters were tuned? How were they adjusted and why?
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?

  
If a well known architecture was chosen:
* What architecture was chosen?
  The LeNet NN seems relatively robust to train, having a combination of a few convolutional layers plus fully connected layers at the end seems to work well 
* Why did you believe it would be relevant to the traffic sign application?
  The traffic signs shoudl have large bold text and clear signs for drivers to identify, in some sense this should be easier than handwriting
* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?
 92% is pretty good accuracy with training, but I think it could be improved with 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

The traffic signs are shown in my writeup 

Several of the images may be difficult to classify because they have text overlaid from Getty Images
I also think several of the images may have problems when cropped and scaled to 32x32 depenfing on interpolation method for scaling (I did experiment with this

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| Comments
|:---------------------:|:---------------------------------------------:| 
| Stop Sign      		| Stop Sign									| 1.00
| Speed Limit 40     			| No Entry										| .99
| Do Not Enter					| Do Not Enter											| .99
| General Caution 	      		|  Slippry Road Possible					 				|
|Children Crossing 	| Keep Right    							|  Possible Resizing Error


This was definitely much lower prediction accuracy than I expected. Only 2 of 5 were correct. Even worse, the missed signs were no where near the accurate prediction. I suspect a few errors
1. Poor resizing and cropping
2,  Use of Greyscale normalization doesn't work as well in compressed (jpg) images
The other thing I don't understand is why no other of the top five probabilities are close. This seems odd.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code is described in cell [31]


Stop_Sign.jpg
StopProbability0.999999
Speed limit (70km/h)Probability4.42543e-07
Turn right aheadProbability1.55205e-07
Speed limit (30km/h)Probability7.1357e-08
Go straight or rightProbability6.11137e-09

speed_limit.jpg
No entryProbability0.999895
No passingProbability9.38304e-05
Bumpy roadProbability8.63144e-06
Priority roadProbability1.85092e-06
Turn left aheadProbability1.47116e-07

Do-Not-Enter.jpg
No entryProbability1.0
Beware of ice/snowProbability3.34336e-20
Turn right aheadProbability5.10891e-21
StopProbability1.10906e-21
Priority roadProbability6.04741e-22

RadfahrerAbsteigen.jpg
Slippery roadProbability0.999966
No passing for vehicles over 3.5 metric tonsProbability3.39801e-05
No entryProbability5.042e-07
Turn right aheadProbability5.30193e-09
No passingProbability4.01927e-09

Watch_for_Children.jpg
Keep rightProbability0.999983
Speed limit (30km/h)Probability1.67906e-05
Dangerous curve to the rightProbability1.20677e-07
Traffic signalsProbability5.46322e-10
General cautionProbability3.32936e-10

