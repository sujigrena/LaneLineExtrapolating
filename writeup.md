# **Finding Lane Lines on the Road** 


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

My pipeline consisted of 6 steps. 

Step 1: I converted the image to grayscale to convert the 3 color channels to 1.


Step 2: Then I applied canny edge detection function to detect all the edges in the given image.

Step 3: After identifying the edges, I applied gaussian blur to remove the noise in the image.

Step 4: Then I applied the region of interest function which finds the region that contains the lane lines in the image.

Step 5: Next, I applied the hough transform to identify the lane lines in the identified region.The hough transform identifies the coordinates of the line to be drawn, by calling the draw-line method.

Mainly I've modified the _draw_line() method to split the coordinates as left and right points based on the slope. Then calculate the average slope of the left and right side lines. Then call the cv2.fitLine to get the x and y vectors respectively.   
After getting this vectors and a point(x,y) in the line as a result, I calculate the left and right slopes and intercepts respectively. Then I push these data to a queue which stores the previous 5 frames to help me identify the lenght of the line segments to be drawn in the current frame. Then I get the calculate the start and end point of the lines using the previous frame details and plot them in the image.

Step 6: Then I add the image with the lines drawn with the actual picture to produce the final result.



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when we encounter curves/turns in the road. The code is developed assuming the road is straight. The lane lines get plotted in an undesired way when we encounter these scenario.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to identify the read the features of the road right rather than assuming the lane lines are always .
