# **Finding Lane Lines on the Road** 

## Diogo Nogueira Knop

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "image example"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The first step was tune the parameters. For Hough Transform: rho, theta, threshold, min_line_length, max_line_gap. For Canny detection: gaussian kernel size, low threshold, high threshold. For this I used the project https://github.com/maunesh/opencv-gui-helper-tool and I add the controls to adjust Hough Transform. After find the best values, I designed the pipeline.

My pipeline consisted of 5 steps:

1) Convert to gray
2) Gaussian Filter
3) Edge detection using Canny
4) Region of Interest
5) Hough Transform

In order to draw a single line on the left and right lanes, I modified the hough_lines() function by adding slope_intercept(). A line has the equation y = mx + b, and if we have two points (x, y), it is possible to calculate the parameters m and b.

m = (y2 - y1) / (x2 - x1)

b = y1 - m * x1

When m is negative, the line is a left lane, otherwise is a right lane. Each line found has the parameters stored in a list. I calculate list average to find the lane equation. Then 2 points are calculate using the parameters to draw the line. 

Also I implemented a moving average for 20 frames to soft the lane changes.

An example of the final result is shown below:

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when no lines were found, or when a horizontal line was found.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to change the pupeline to work properly with the Challenge video
