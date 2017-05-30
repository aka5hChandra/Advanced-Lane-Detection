

**Advanced Lane Finding Project**


[//]: # (Image References)

[image1]: ./ouput_images/undistorated.jpg "Undistorted"
[image2]: ./output_images/test1.jpg "Road Transformed"
[image3]: ./output_images/threshold.jpg "Binary Example"
[image4]: ./output_images/warped.jpg "Warp Example"
[image5]: ./output_images/color_fit_lines.jpg "Fit Visual"
[image6]: ./output_images/test_images/test6.jpg "Output"
[video1]: ./output/project_video.mp4 "Video"


### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the first code cell of the IPython notebook located in "project4.ipynb" 

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][image1]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

Below is the example of distotion corrected image
![alt text][image2]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I have used the few utility functions which have used in combination to generate a binary image (thresholding steps at lines 186 through 273 of cell 3), where I have put together a pipeline to apply thresholding.  Here's an example of my output for this step.  

![alt text][image3]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

The code for my perspective transform includes a utiltiy function called `warpImage`, which appears in lines 314 through 330 in cell 3 .  The `warpImage()` function takes as inputs an image (`img`), as well as source (`src`) points.  I have used the lane detection by using hough lines from project 1 to find the src pooints and have hardcode the destionation points


I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![alt text][image4]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

I have used the utility function `slideWindow()` in line 330 of cell 3 to find the lane line pixel, in this method I have implemented the sliding window algoritam to find the potential pixels of lane line and used these pixel cordinates to fit the lane lines

![alt text][image5]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I have used the formula discribed in lecutre to find the readius of cauvature of lane and used for sanity check of detect lane lines.  I did this in lines 439 through 444 in my code in cell 3.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in lines 497 through 503 in my code in cell 3 in the function `slideWindow()`.  Here is an example of my result on a test image:

![alt text][image6]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

The major problem I have faced is in finding the perfect threshold of image , my thresholding pipeline fails to find the lane lines when there is heavy shadow or relativly brigther road, as a consequance polynomial fit fails and which is evident in wobbling of lane in vedio.
