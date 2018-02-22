# **Finding Lane Lines on the Road - Mithran Mathew** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My processing oipeline consists of 5 steps - see notebook for more details
**** Basic Pipeline  ****
1. Work on a copy
2. Threshold - Apply Gaussian (Blur) Filter, Canny Filter to find edges
3. Apply Region of Interest to Lanes
4. Find all clear lines of lane
5. Average all lines to 2 - positive and negative slope of left and right lane
6. Combine source and processed image, output files

The draw lines function used an extrapolate line function, as well as an average_lines function.
The extrapolate function extended the line down and up past the region of interest using the y=mx+b slope equation
The average lines function tried to group lines into negative (left lane) and positive (right lane) lines, 
then average the x and y of each group and report two averaged lines for left and right lane respectively


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

 My pipeline still doesn't work on the challenge video.  I did try to make all region of interest 
 components parameterized based on image size, but some of the image processing steps especially would need to be retuned still

 The other assumption is the lanes critical identifiers are in the lower half of the image.  Region of interest was scaled by this.
 This seems generally true looking at the camera location of the test videos and images, but might not be correct for all placements.



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to make the challenge video work.  The camera placement seems to be foiling my estimator of lanes!

Another potential improvement could be to  make the challenge video work
