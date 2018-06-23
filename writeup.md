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

My pipeline consisted of 5 steps. 

First, I separating line segments by their slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line. For left line, the slope should above 0, and for right line, the slope should below zero. Meanwhile, I give limint  range for (y2-y1)/(x2-x1), so part of the noise can be filtered out.

Second, I calaculted the line slope m and b of each Hough line by using np.polyfit.  (refers to y=mx+b)

Third, I calaculate the average value of m and b of all Hough line.

Fourth, I signed y1=image.shape[0] as the bottom point of the slope, and siged y2=int(y1*0.63) as the top point of the slope, and by using line eqotation mentioned in Third step, I calaculate x1, and x2 with x=(y-b)/m.

Fifth, I draw up the line by using cv2.line, and above mentioned points.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be the top point of the slope line is not so accurate, because I set the y2 is a kind of fixed value.

Another shortcoming could be the draw up line is not perfectly match the real line on the road, when the vechicle pass the none-straight road (pass a turn or a corner).


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to draw up line by several continous line segments to have better performance in turn or corner.

Another potential improvement could be to add conditions to judge if slope or b change severely when do vedieo processing, then maybe helpful to judge if the draw up line for every sigle image is correct.
