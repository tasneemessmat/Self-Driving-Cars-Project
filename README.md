# Self-Driving-Cars-Project
Image Processing Project

# Lane_Detection_Computer_Vision
 ## Advanced Lane Finding

---

Overview
---

Pipeline used for lane line detection :
* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

Installations
---

1. Install Anaconda on your local setup (Choose Python 3 version - [Link](https://www.anaconda.com/distribution/))
2. Install Libraries :
OpenCV : `> conda install -c conda-forge opencv `
moviepy (used in this project to work with videos): `> pip install moviepy`

# Steps

### 1)Undistoring images 


### 2)Thresholding - Color thresholding and Gradient thresholding



### 3)Perspective and Inverse perspective transform (bird Eye)


### 4)Lane line identification


### 5)Curvature Detection

All the functions under "Helper functions" are used to identify lane lines.

__`find_lane_pixels()`__

The function `find_lane_pixels()` used to calcuate both lanes x and y pixels that lie within a window. only for the first frame of the video this function is run. from the next frame onwards only pixels in the vicinity of the previously detected lane  are analysed to be part of lane more on this later.

if used to detect lane on only image then only `find_lane_pixels()` will be called by default which uses sliding window techique.

##### Steps taken to detect line using sliding window technique

__Hyperparameter for window:__
* nwindows = 9
* margin = 100
* minpix = 50

* __step 1:__ Get the histogram of warped input image


* __step 2:__ find peaks in the histogram that serves as midpoint for our first window
* __step 3:__ choose hyperparameter for windows
* __step 4:__ Get x, y coordinates of all the non zero pixels in the image
* __step 5:__ for each window in number of windows get indices of all non zero pixels falling in that window
* __step 6:__ Get the x, y coordinates based off of these indices


__`fit_poly()`__

This function fits the points on a 2nd order polynomial

Given x and y coordinates of lane pixels fir 2nd order polynomial through them
    
here the function is of y and not x that is
    
x = f(y) = Ay**2 + By + C
    
returns coefficients A, B, C for each lane (left lane and right lane)

__`search_around_poly()`__

This function is extension to function `find_lane_pixels()`.
    
From second frame onwards of the video this function will be run.

the idea is that we dont have to re-run window search for each and every frame.
    
once we know where the lanes are, we can make educated guess about the position of lanes in the consecutive frame,
    
because lane lines are continuous and dont change much from frame to frame(unless a very abruspt sharp turn).
    


* Finally all the images are merged together into one output video showing it's pipeline
