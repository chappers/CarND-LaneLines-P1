### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

<!-- My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1] -->

The process for my pipeline is in two stages:

1.  Detect lanes without lines drawn in
2.  Draw in/extrapolate the lane lines

With the first stage the steps are:

1.  Firstly process using median blur to get rid of anything noisy
2.  Convert anything that "looks" like yellow to white, to detect yellow lines better
3.  Convert to grayscale
4.  Apply gaussian blur
5.  Apply canny edge detection
6.  Subset by region, estimated by a trapezoid
7.  Apply hough transform

With drawing in the lines, I used the output from the previous stage

1.  Taking only the hough transform, repeat with canny, being more aggressive with threshold
2.  Dialate the solution to get "solid" lines
3.  Repeat with canny again
4.  Use hough transform to get the lines
5.  Use a modified `draw_lines` function draw in and extrapolate the lines. 

The new `draw_lines` function:

1.  Uses clustering to determine which sets of points belongs with which  "line"
2.  Uses `cv2.fitLine` to fit a line
3.  Draws it based on the fitted line.


### 2. Identify potential shortcomings with your current pipeline

The lane line markings are not as smooth as the example, and have a tendency of jumping all over the place. 



### 3. Suggest possible improvements to your pipeline

Since we use clustering iteratively to determine the line segment groupings it sometimes gets it wrong. It might be better to either:
*  Keep history, so that it gets better over time
*  Use a rule based approach so that it is consistent

Generally understanding roughly the location of lines in the previous frame should help inform where new lines are now at!


