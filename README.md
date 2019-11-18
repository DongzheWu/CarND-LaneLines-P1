# **Finding Lane Lines on the Road** 




### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I blurred the images and used canny function to detect edges. And I masked some areas, then I applied a Hough Transform to detect lines. Finally, I superimposed original images and the images that have lines.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating slopes of lines which were detected by Hough Transform function and judging the slopes of lines are postive or negative. If they are postive, then the lines are on the right lanes, vice versa. I realized that when there was no any right lines or left lines detected. And in this case, errors will come out, since some x array are null. So I chose to filter x arrays which are null. I also found that some lines (slopes are between 0 to 0.3, 0.8 to 1) were detected. In this case, when I use np.polyfit to fit all points, the slope of the line I got has a big difference from the real lane. So I chose to filter the lines which have slopes are between 0 to 0.3, 0.8 to 1.
[1][whiteCarLaneSwitch](/test_images_output/whiteCarLaneSwitch.jpg)
"whiteCarLaneSwitch"
[2][image](test_images_output/solidYellowCurve.jpg "solidYellowCurve")
[3][image](test_images_output/solidWhiteCurve.jpg "solidWhiteCurve")
[4][image](test_images_output/solidWhiteRight.jpg "solidWhiteRight")
[5][image](test_images_output/solidYellowLeft.jpg "solidYellowLeft")
[6][image](test_images_output/solidYellowCurve2.jpg "solidYellowCurve2")


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is that my pipeline worked not very well with the video of solidYellowLeft, because some lines which have totally different slopes from the real lanes were detected. These line affected the performance of np.polyfit.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to draw average line which has average slope of all lines, instead of using polyfit function.

Another potential improvement could be to calculate average slope of all lines, and filter points of lines which have very different slope compared to the average slope. Since I need to submit the project to meet deadline, I will try this improvement later.
