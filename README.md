# TP Visión Artificial 2022

## Members

- Alejo Ramirez Gismondi
- Katia Cammisa
- Matías Gayo
- Numa Leone

## Air Draw Revamped

<p style="text-align: justify; margin-bottom: 20px; margin-top: 20px;">
This project was created from a fork of <a href="https://github.com/arefmalek/airdraw">arefmalek/airdraw</a> as a base. Details about implementation can be found after the Setup section.
</p>

### Setup
<b>NOTE</b> This setup is just for what I use (Ubuntu 20.04). While I am willing to bet this will work for windows and unix, just be safe!
#### Virtual environment
`python3 -m venv venv`
#### Install Dependencies
`source ./venv/bin/activate`

`pip3 install -r requirements.txt`
#### Run program
`python3 airdraw.py`

## Demostration Video

![Demo of us trying out the hands](./demo_gifs/demonstration.gif)

## Inner workings

The original code was forked from arefmalek/airdraw.
This repository provided the base of Airdraw, making use of mediaPipe to detect a hand and then using OpenCV to draw.

The original gestures were changed from the original ones (can bee seen below in the "Old Available Gestures" section.

The lines are drawn both over the image and in a separate canvas, from which OpenCV is used to detect the outermost contour of the drawing.

Having the drawings in a separate canvas provides us with an image free of noise, which makes detecting the figures easier

The contour is then processed by the machine learning model, which can detect between triangles, stars and rectangles.

In order to provide more stability for the model, the last 60 predictions are stored and the result is the average prediction of that list. This has some drawbacks, such as delayed detection time, although it compensates with more stability for the result of the prediction.

## New Gestures

### Drawing

Join the middle finger with the index as shown in the video above

### Erasing

Join the thumb with the index and erase with the middle finger. The bigger the distance between the index and the middle finger, the bigger the eraser

### Hovering

To hover, you must do any other hand gesture as longs as it is different from the Drawing and Erasing ones. In this mode, you can select any of the 3 colors to draw, by hovering into the box colors at the top of the screen.

You can also hover into the Clear all button to delete all the drawings.

## Old Demonstration

![Demo of my trying out the hands](./demo.gif)

## Old Available Gestures

### Drawing
![Drawing directly on screen](./demo_gifs/drawing.gif)

### Hovering
![Hovering over drawings on screen](./demo_gifs/hovering.gif)

### Erasing
![Erasing earlier drawings on screen](./demo_gifs/eraser.gif)

### Why?
I've seen tons of attempts of this sort of thing with HSV masks, and while it's more true to image processing that openCV caters for, I was sort of against letting our own styluses [go to waste](https://money.cnn.com/2015/09/10/technology/apple-pencil-steve-jobs-stylus/index.html).
Once I found out about [mediapipe](https://google.github.io/mediapipe/), I decided I would give this thing a shot! What you see is my attempt at materializing the idea, there is a more detailed [writeup](https://arefmalek.github.io/blog/Airdraw/) on my blog. 

### How?
Like I mentioned before, the ML workhorse here is definitely mediapipe. They've got awesome ML solutions so we can quickly gather data on the hand and use what we gather rather quickly. Other than that I pretty reliantly used OpenCV for image manipulation and NumPy for some basic dot products and because OpenCV uses numpy to represent images.

The conversion from hand data to lines / functionality is primarily done with some Python, basic linear algebra, and OpenCV. I'll leave the rest in the blog post. 

### What's next?
Truthfully, I'm not too sure. I got a ton of great suggestions, and I've been battling the urge to just change the whole repository to C++ instead of Python (only hesitating factor was setting up CMake honestly). If anyone is willing to get started on it, please feel free to fork / put up a Pull Request! 

Thanks for reading :)
