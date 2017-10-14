# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src= "https://github.com/JeffGoodrich9791/CarND-Finding-Lane-Lines/blob/master/output_solidWhiteCurve.jpg" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. 


Creating a Great Writeup
---
For this project, a great writeup should provide a detailed response to the "Reflection" section of the [project rubric](https://review.udacity.com/#!/rubrics/322/view). There are three parts to the reflection:

1. Describe the pipeline
The pipeline was built using the following code: 

def process_image(img):
   
        imshape = img.shape
        gray = grayscale(img)
        blur_gray = gaussian_blur(img, 3)
        edges = canny(blur_gray, 100, 150)
        
        
        vertices = np.array([[(0,imshape[0]),(465, 320), (475, 320), (imshape[1],imshape[0])]], dtype=np.int32)
        masked_region = region_of_interest(edges, vertices)
        
        lines_image = hough_lines(masked_region, 2, np.pi/180, 15, 25, 2)
        
        result = weighted_img(lines,img,a=0.8, B=1.0)
        
        return result
        
2. Identify any shortcomings

The initial code ran I ran with defining the area of interest or "masked_region" in the code used a weighted function of the x1, x2, y1, y2, m1, and m2 to determine the vertices. I found this code to sometimes grab the background in part of the vertices and caused the lines to temporarily sway from the actual lines on the road and cross paths. 

3. Suggest possible improvements

I fixed this issue by using the np.array function in the "def process_image(img)" pipeline with actual coordinates for the x1,x2, y1, y2 lines as used in the first example of the course!  


The Project
---

## The Project consists of the following essential steps for beginning the Udacity Self-Driving Car Engineer Program ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7).

In this project you will detect lane lines in images using Python and OpenCV. OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.

Creating the environment with Anaconda

To do this project, you will need Python 3 along with the numpy, matplotlib, and OpenCV libraries, as well as Jupyter Notebook installed.

We recommend downloading and installing the Anaconda Python 3 distribution from Continuum Analytics because it comes prepackaged with many of the Python dependencies you will need for this and future projects, makes it easy to install OpenCV, and includes Jupyter Notebook. Beyond that, it is one of the most common Python distributions used in data analytics and machine learning, so a great choice if you're getting started in the field.

Choose the appropriate Python 3 Anaconda install package for your operating system here. Download and install the package.

If you already have Anaconda for Python 2 installed, you can create a separate environment for Python 3 and all the appropriate dependencies with the following command:

> conda create --name=yourNewEnvironment python=3 anaconda

> source activate yourNewEnvironment

Installing OpenCV

Once you have Anaconda installed, first double check you are in your Python 3 environment:

>python
Python 3.5.2 |Anaconda 4.1.1 (x86_64)| (default, Jul 2 2016, 17:52:12)
[GCC 4.2.1 Compatible Apple LLVM 4.2 (clang-425.0.28)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
(Ctrl-d to exit Python)

run the following commands at the terminal prompt to get OpenCV:

> pip install pillow
> conda install -c https://conda.anaconda.org/menpo opencv3

then to test if OpenCV is installed correctly:

> python
>>> import cv2
>>>
(Ctrl-d to exit Python)

Step 3: Installing moviepy

We recommend the "moviepy" package for processing video in this project (though you're welcome to use other packages if you prefer).

To install moviepy run:

>pip install moviepy

and check that the install worked:

>python
>>>import moviepy
>>>
(Ctrl-d to exit Python)


**Step 2:** Open the code in a Jupyter Notebook

You will complete the project code in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

This project is completed in a Jupyter notebook. If you are unfamiliar with Jupyter Notebooks, check out Cyrille Rossant's Basics of Jupyter Notebook and Python to get started.

Jupyter is an ipython notebook where you can run blocks of code and see results interactively. All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, run the following command at the terminal prompt (be sure you're in your Python 3 environment!):

> jupyter notebook

A browser window will appear showing the contents of the current directory. Click on the file called "P1.ipynb".  

**Step 3:** Complete the project and submit both the Ipython notebook and the project writeup


