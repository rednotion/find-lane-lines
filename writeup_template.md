# **Finding Lane Lines on the Road** 

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

**Pipeline**
1. Convert to grayscale, smooth and find Canny edges
2. Convert another copy to HLS and use the S channel to find another set of Canny edges
3. Combine the edges found in (1) and (2)
4. Apply region masking to focus on the triangle of space nearest to the user
5. Find 4 end points to draw the two lane lines
6. Combine the lane-line image from (5) with the original image to obtain final output

[image1]: ./examples/grayscale.jpg "Grayscale"

![breakdown of steps]['./test_images_output/breakdown.png]

**`

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
