# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[breakdown_image]: ./test_images_output/breakdown.png "Breakdown"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

**Pipeline**
1. Convert to grayscale, smooth and find Canny edges
2. Convert another copy to HLS and use the S channel to find another set of Canny edges
3. Combine the edges found in (1) and (2)
4. Apply region masking to focus on the triangle of space nearest to the user
5. Apply Hough Transform to find the lines/edges based on the combined and masked output at step 4
6. Find 4 end points to draw the two lane lines
7. Combine the lane-line image from (5) with the original image to obtain final output

*The image below shows a breakdown of some of the key steps 1, 2, 5, and 7* 

![breakdown][breakdown_image]


**Step 6: Finding the end point to draw lane lines i.e. modifying `draw_lines()`**

To draw continuous lane lines, 

1. I broke the hough output into 4 regions: top left, bottom left, top right, bottom right. 
2. In each of those regions, I found the average point (average X and Y value). 
3. Then, on each side (left and right), I used the two points to calculate the gradient and the intercept. 
  - gradient (m) = (x1-x2)/(y1-y2)
  - y = mx + b --> intercept = y - mx
4. Then, I could calculate the end points of each lane by substituting the value for `x` (in this case x will be **height** of the image)
  - one value would be at the very bottom edge of the image, hence height = `image.shape[0]`
  - the other value would be at the midpoint of the image (where the view of the road meets the sky!), which I set to a multiple of the image height (e.g. `0.5*image.shape[0]`
5. Finally, I sub these points back into `cv2.line()` function to draw the lines on the image.

### 2. Identify potential shortcomings with your current pipeline

- "Hard coding" the masking region can be dangerous, especially when extrapolating how long the lane line should be 
- Cannot detect curves! (also related to previous point -- might draw a straight line right through the curve)
- **Challenge image**: Managed to deal with some issues due to the hood of the car by adjusting mask, and with the yellow lane by using the S-channel in HLS, but still performs badly when there are things like shadows in the image.

### 3. Suggest possible improvements to your pipeline

- Account for curves in the road/different lane lengths
- Make use of data in previous frames! e.g. the lane detected between frame `i` and `i+1` shouldn't be too different/hopping across too many pixels. It should only change gradually. This will also allow us to reduce noise (especially frames where there might suddenly be shadows and other objects, like in the challenge video)

Another potential improvement could be to ...
