# CarND-Finding-Lane-Lines-on-the-Road

**Finding Lane Lines on the Road**

## The goals / steps of this project are the following:
1. Read an image
2. Use and modify helper functions to process the images
3. Test images using code explained in the Udacity course
4. Build a lane finding pipeline for video feed
5. Test the pipeline using moviepy
6. Save and write the file to an output directory
7. Reflect on the work performed in a written submission

### Relection

1. Describe the Pipeline: As part of the description, explain how you modified the draw_lines() function

Building the pipeline consisted of the following steps in order: 

* Converted the image to grayscale

```sh
gray = grayscale(img)
```
* Implemented GaussianBlur by passing argument into function
```sh
gray = gaussian_blur(img, 3)
```
* Defined edges using Canny 
```sh
edges = canny(gray, 100, 150)
```
* Defined vertices for the masked area
```sh
imshape = img.shape
vertices = np.array([[(.51*imshape[1], imshape[0]*.58), (.49*imshape[1], imshape[0]*.58),(0, imshape[0]),(imshape[1], imshape[0])]], dtype=np.int32)
```
* Defined masked region of interest
```sh
masked_area = region_of_interest(edges, vertices)
 ```
* Defined HoughLines and Weighted Lines functions
 ```sh
lines = hough_lines(masked_area, 2, np.pi/180, 25, 55, 5)
result = weighted_img(lines,img,a=0.8, B=1.0)
  ```
 * Return result
 ```sh
 return result
 ```

 ## Next: Process the Video

* Import tools needed to process the video
```sh
# Import everything needed to edit/save/watch video clips

from moviepy.editor import VideoFileClip
import imageio
imageio.plugins.ffmpeg.download()
from IPython.display import HTML
```
* Process the video and save to output file
```sh
white_output = 'test_videos_output/solidYellowLeft.mp4'
## To speed up the testing process you may want to try your pipeline on a shorter subclip of the video
## To do so add .subclip(start_second,end_second) to the end of the line below
## Where start_second and end_second are integer values representing the start and end of the subclip
## You may also uncomment the following line for a subclip of the first 5 seconds
##clip1 = VideoFileClip("test_videos/solidWhiteRight.mp4").subclip(0,5)
clip1 = VideoFileClip("test_videos/solidYellowLeft.mp4")
white_clip = clip1.fl_image(process_image) #NOTE: this function expects color images!!
%time white_clip.write_videofile(white_output, audio=False)
[MoviePy] >>>> Building video test_videos_output/solidYellowLeft.mp4
[MoviePy] Writing video test_videos_output/solidYellowLeft.mp4
100%|█████████▉| 681/682 [00:45<00:00, 14.42it/s]
[MoviePy] Done.
[MoviePy] >>>> Video ready: test_videos_output/solidYellowLeft.mp4 

CPU times: user 21.3 s, sys: 3.46 s, total: 24.7 s
Wall time: 47 s
```













