
# **Finding Lane Lines on the Road** 

## The first Project of the Self-Driving Car Engineer Nanodegree

### A self driving car needs to find the lane lines in order to stay within them. This is a first shot.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### Description of my Pipeline

My pipeline consists of 5 major steps:

1. Converting the images to grayscale. I also tried taking the maximum colour value per pixel which I think should help to select yellow lines as good as white ones, but it didn't really show any impact.
2. Using Canny edge detection to find lines in the image. I decided against applying an additional Gaussian kernel beforehand because I couln't observe improvements in doing so. I guess the one applied internally does a pretty good job already.
3. Applying a mask to search for lines only in a region of interest and lose "noise". The way the parameters of the vertices are defined may seem a little weird. The reason for this is that the last video, challenge.mp4, came in a different resolution (only in the github version) which forced me to make the code more generic with little effort.
4. Calculating Hough lines. A lot of parameters were tried but, unfortunately, no combination made the pipeline completely succeed the challenge.
5. Draw the lange lines. For this I modified the draw_lines() function such that
	i) All the different lines segments were sorted by their slope to either belonging to the left or the right lane. Lines that were assumned to be not steep enough to be part of a lane were discarded
	ii) Lines were filtered for outliers based in their slope. (Didn't seem to be many)
	iii) A representative line was calculated by averaging over the remaining sloped and the centers of the associated lines.
	iv) This line was extended to start at the bottom of the picure and go up till the lowest value of y that was found in any line.

### 2. Identify potential shortcomings with your current pipeline

When the contrast is not good anymore, it does not work too well as can be seen in the last video.

It would probably not work for sharp curves where the lane is not straight or steep roads where te region of interest does not fit anymore.

The lines were a bit fuzzy, i.e. didn'd change smoothly between two images.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to to further investigate how the edge detection can be improved in said problematic case.

Another improvement might be to connect the information of subsequent images. Thus it might be possible to make the line appear to be drawn more smoothly and probably also interpolate regions with to little information for line drawing. As this is whished for, however, is a different question since no line might be sign of an obstacle which should better be found.
