# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./DrawLinesOnLanesOutput.png "Output image after detecting lane lines after averaging"
[image2]: ./DrawLinesOnLanesBeforeAvg.png "Output image after detecting lane lines before averaging left and right lines"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. This pipeline assumes all the images are of the same size. 
* First I converted the image to grayscale. 
* On the grayscale image, I used the gaussian_blur() helper function with a kernel size of 9 to help detect the right edges and gradients * in the image. After trying out a kernel size of 5,7 and 9, I felt 9 gave me an optimal image. 
* After using the gaussian_blur() helper function, I ran the canny() helper function to detect edges in the gaussian blurred image
* Since we do not want to detect lines in the entire image, we can create a region of interest using the region_of_interest() function which takes in the canny edge image and uses an open CV function called cv2.fillPoly to create a region of interest by taking in vertices *from the user. We can create a masked image from this. 
* We not have to perform a hough transform on the image to find lines. Hough transform provides us with different parameters like rho, theta,min line width, max line gap etc.. to help identify the set of lines we want detected. Tuning these parameters will help us identify the right set of lane lines.
* In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the average left and right slopes for the lines identified by the hough transform. Below is an image showing the output after the draw_lines() function has been applied to the image after following the steps above. If we do not average the lines that are detected through the hough transform, the output would look like 2nd image. 

![alt text][image1]
![alt text][image2]


### 2. Identify potential shortcomings with your current pipeline


* One potential shortcoming would be what would happen when the lane lines are not straight and have a curve to it, this algorithm might not be sufficient to accurately detect lane lines. 

* Another shortcoming could be that if you do not tune your hough line parameters accurately, it might not detect enough slope points for the lines and the algorithm might exit out and produce NaN

* This pipeline assumes all the images are of the same size and if we have different sizes.


### 3. Suggest possible improvements to your pipeline

* A possible improvement would be to consider transforming the image to a different view and then also consider the curvature of the road.

* We need to consider the possibility of reshaping the images to all be of the same size.
