# CarND-P1 Finding Lane Line

## Description

**This my 1st project result of Udacity self-driving car nanodegree (CarND) term 1. It required implementing a lane line finding software to detect lane line in a sequence of video.**

* Udacity self-driving car nanodegree (CarND) :

  https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013


### Lane line detection pipeline 

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I apply Gaussian smoothing to let edges features easier to find. Afterwards, I use Canny edge detection to find edges, then mask out uninterested region using 4 sided polygon. Then, hough transform is applied to find the line segments. In the end, I modify the draw_lines() function to average line segments to form left and right lane line and combine the 2 line with original image to form an annotated image.

#### 1. Gray scale conversion

![alt text][image1]

#### 2. Gaussian smoothing

![alt text][image2]

#### 3. Canny edge detection

![alt text][image3]

#### 4. Polygon region of interest applied

![alt text][image4]

#### 5&6. Hough transform and draw annotated image

![alt text][image5]

In order to draw a single line on the left or right lanes, I modified the draw_lines() function by :
1. find segment whose slope between -0.6 and -0.9 to be averaged and find the average left lane line slope

2. find segment whose slope between 0.45 and 0.75 to be averaged and find the average right lane line slope

3. Average the left line segments' points to get an average point that left lane line will go through, and same method is applied to right line segments.

4. Since getting average point and slope, I calculate 2 point position along the line on bottom and half height of the image. Left lane line and right lane line are done in the same method.

5. Finally, I connected the 2 points to form the line. Both left and right lane line are drawn.


### Shortcomings of current pipeline

One potential shortcoming would be lane line not found when most of line segment slopes are out of range I restricted.


### Possible improvements to current pipeline

A possible improvement would be to record previous frames’ lane line slope and adjust the slope range based on it because the adjacent frame’s lane line slope shouldn’t vary greatly.