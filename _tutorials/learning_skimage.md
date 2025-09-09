---
title: "You should learn scikit-image before learning OpenCV"
---

If you are a plant scientist looking to build skills in computer vision/image analysis, you will naturally wonder where to start. There are three places to start.

PlantCV is a library built 

I feel that  library `scikit-image` first.

If you're new to image analysis, these are  good reasons to learn `skimage` from the beginning. If you're used to using `cv2`, there are several reasons to consider picking up `skimage` as your default choice when starting a new imaging project.

The [opencv-python library](https://pypi.org/project/opencv-python/), aka `cv2`, is the most widely used library for basic image processing in python. It's mostly a wrapper around the actual `opencv` library written in C++, which has existed in various forms since ~2000. Much of the documentation for `cv2`.

A close second is [scikit-image](https://scikit-image.org/), aka `skimage`. This is a library written in python (with some Cython in the mix), so its modules and functions are organized around pythonic principles.

If you're new to image analysis, these are  good reasons to learn `skimage` from the beginning. If you're used to using `cv2`, there are several reasons to consider picking up `skimage` as your default choice when starting a new imaging project.

I find `skimage` to be easier to learn, easier to use, and generally more powerful.

This tutorial outlines some of the reasons you might want to use `skimage` instead of `cv2` and shows a step-by-step comparison of the code for several basic image processing functions.


*Note:* If you do a lot of image analysis, you will likely have to learn both libraries at some point. Both libraries have pros and cons.

*Note:* There is a third widely-used image handling library: the Python Imaging Library (`PIL`), commonly used in the form of [Pillow](https://pypi.org/project/pillow/), a fork of `PIL`.

`PIL` is designed for common image transformations like resizing, cropping, changing colorspace, etc. It stores images as a specific `Image` class, with a large number of class-specific methods to handle these operations.

By contrast, `cv2` and `skimage` treat images as `numpy` arrays, *n*-dimensional matrices of values that can be handled like any other matrices. They each have a wide array of tools for more complex image analysis methods.

`PIL` is great at handling input/output - if your images are in a weird format and you're not sure how to read them in, try `PIL`.

## Reasons to prefer skimage

* Better documentation
* Simpler, more intuitive functions and syntax
* pythonic tools make things clearer

# Better documentation

# Python-native organization

# Import and export

# thresholding

# saving etc.