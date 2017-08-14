# **Finding Lane Lines on the Road** 

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
Here’s how original image looked like:

My pipeline consisted of 6 steps. 


a. First, I converted the images to grayscale.













b. Next, I applied Canny method to detect edges I used low_threshold=50 and high_threshold=100. 


c. I then created a triangle like polygon to define area of interest and mask edges detected outside the region of interest




d. After that, I applied hough transform to detect lines. Lot of iterations were required to optimize parameters involved. Here, I also removed lines whose slopes were between -0.3 and +0.2 (found through iterations).

e. In order to draw a single line on the left and right lanes, I modified the draw_lines() function - I averaged lines to join dotted lines. Here, I divided lines into two categories (+ve slope and –ve slope) and used cv2.fitline to find average slope and intercept of the two lines.


f. I then overlaid the line images with original image.

 
Clip.f1_image was used to process the series of frames from the video, where each frame went through series of steps above and produced lines and integrated all of them back to form the output video. 

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is significant change in the direction of the road – for instance, we are using a triangle like polygon to map the area of interest. This may have to be made more dynamic depending upon the road.

Another shortcoming could be detecting the curves – for instance, the curves under the challenge video are not detected completely. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to improve Hough transform parameters for it to detect curves existing in challenge video.

Another potential improvement could be to use average slope and intercept from previous few frames to draw average lines. For instance in some instances, we see a slight jump in lines slopes.
