# PhotoLab v1.0

Implementation of the PhotoLab v1.0 project

The russian version of the task can be found in the repository.

## Contents

1. [Chapter I](#chapter-i) \
   1.1. [Introduction](#introduction)
2. [Chapter II](#chapter-ii) \
   2.1. [Information](#information)
3. [Chapter III](#chapter-iii) \
   3.1. [Part 1](#part-1-implementation-of-simple-filters-in PhotoLab-v1.0) \
   3.2. [Part 2](#part-2-implementation-of-convolution-filters-in-photolab-v10) \
   3.3. [Part 3](#part-3-bonus-implementation-of-color-correction)


## Chapter I

![PhotoLab1.0](misc/images/PhotoLab_v1.0.jpg)

> A filter (from Latin filtrum) is a device designed to separate something from something. For example, mechanisms that separate (or remove) from a given source object some part with predetermined properties. \
> *There are other meanings of this term, see Filter.*

*Next*

*-- ...The most common way to purify water is to use a pitcher filter. It does not require any installation and is easy to replace...*

*Skip*

*-- ...Cardboard is the most common material for air filters. However, in some countries replacement elements are made of synthetic fibers. Operation...*

*Skip*

> The principle of the biological filter (biofilter) is based on the natural ability of living micro-organisms (bacteria, plants) to extract and/or recycle organic and inorganic volatile substances from the impurities passing through them.
This involves artificially produced organic chemicals, oxidation and their decomposition to water and carbon dioxide.

*Next*

> Filtering is also used for computer images. Filtering in this case is understood as an operation which results in an image of the same size, which is obtained from the original image by some rules (filters).

Under this description, you could see many pictures, which certainly caught your attention. They showed the results of different filters, from black and white and contrast, to blurry and abstract.

*- Interesting, that must be how nearsighted people see the world,* - you thought to yourself while looking at the blurred image of a man in front of what looks like the Eiffel Tower. - *It is necessary to study the mechanisms and how they can be implemented.*

## Introduction

In this project you need to implement a program that applies various convolution filters to an image.
Such filters are used for blurring, sharpening, contours, creating a bas-relief effect and applying many other different effects.


## Chapter II

## Information

As you have already understood from the 3D model viewer projects - any raster image is a matrix of pixels. Each pixel has its own color. In some cases, there is a need to apply some effect to the image. This process is called image filtering because each pixel (raster) of the image passes through some computational filter.
Of course, you can simply double, for example, the red channel intensity of each raster, and you will get a slightly redder image. But it is obvious that such fixed filters do not do much.
But what variable arguments, that depend on some attribute of each raster, can be used for pixel-by-pixel filtering?
 
For convolution filtering, it is proposed to use the colors of neighboring pixels. A tool like this is much more powerful, and you’ll see later that it allows you to apply a wide range of effects to your images. Of course, convolution filtering is only a certain algorithm, while the structure of the convolution itself determines the effect imposed on the image.

**The filter kernel** is some weighting matrix overlaid on top of the matrix on the _i,j_ raster of the main image so that the central element of the matrix matches the raster at the _i,j_ position of the main image. Each element of the filter kernel not only determines which pixels affect the color of the _i_ or _j_ pixel, but is also responsible for the weight, that is, how much this element of the kernel affects the _i_ or _j_ raster. Applying the same formula, but with a shifted convolution, you get new pixel color values for each pixel of the image, which are entered in the filtered image matrix.

![s21_kernel](misc/images/kernel.png)

Technically, the formula looks like this:

$`b_{i,j} = \sum^{m}_{p=0} \sum^{n}_{q=0} a_{i-(m-1)/2+p , j-(n-1)/2+q} \cdot k_{p,q}`$, 

where $`a_{i,j}`$ is an element of the original image,

$`b_{i,j}`$ is an element of the filtered image,

$`k_{i,j}`$ is an element of the filter kernel

$`m, n`$ is the width and height of the filter kernel

In practice, this means that the color of each pixel is equal to the sum of respectively multiplied parts of the original image raster and filter kernel elements.

You can achieve completely different effects just by changing the convolution itself, i.e. the size of the matrix and its contents. See **materials** for examples of convolutions.


## Chapter III

## Part 1. Implementation of simple filters in PhotoLab v1.0

You need to implement the PhotoLab v1.0 program:

- The program must be developed in C++ language of C++17 standard 
- The program code must be located in the src folder
- When writing code it is necessary to follow the Google style
- Classes must be implemented within the `s21` namespace
- Prepare full coverage of modules that implement the business logic of the application with unit-tests using the GTest library
- The program must be built with Makefile which contains standard set of targets for GNU-programs: all, install, uninstall, clean, dvi, dist, tests. Installation directory could be arbitrary, except the building one
- GUI implementation, based on any GUI library with API for C++17: Qt, SFML, GTK+, Nanogui, Nngui, etc.
- The program must be implemented using the MVC pattern, and also:
     - there should be no business code in the view code
     - there should be no interface code in the controller and the model
     - controllers must be thin
- You cannot use ready-made libraries that implement filtering or work with matrices, except for the `s21_matrix` library you developed earlier.
- The program should provide the ability to:
    - Load an arbitrary image in BMP format
    - Save the result of filtering into a separate file (BMP format)
    - Apply a filter from a pool of ready-made filters:
        - Conversion to grayscale (without convolution)
        - Negative (without convolution)
        - Toning (similar to grayscale conversion, but in shades of the color specified on the palette. The palette must contain at least 16 different colors. The palette is implemented arbitrarily)
- After applying the filtering, the result should be displayed in the user interface along with the original image

## Part 2. Implementation of convolution filters in PhotoLab v1.0

You need to modify the PhotoLab v1.0 program to implement convolution filters:

- The program should provide the ability to apply the following convolution filters to the image:
    - Emboss 
    - Sharpen 
    - Box blur
    - Gaussian blur 
    - Laplacian filter
    - Prewitt filter (Prewitt filter) or Sobel filter (Sobel filter)
- The program should provide the ability to enter an arbitrary filter kernel matrix (up to size 16x16) by hand through a separate dialog window

## Part 3. Bonus. Implementation of color correction

You need to modify the PhotoLab v1.0 program to implement color correction algorithms:

- The program should provide the ability to make adjustments to color correction, such as:
    - changing the brightness and contrast of the image
    - work with saturation for the whole image (by HSL and HSV models)
- The interface for color correction of the original image should provide the ability to set brightness, contrast and the three parameters of the specified saturation model both numerically and by slider.

💡 [Tap here](https://forms.yandex.ru/u/635a92f584227c1bd824b1b6/) **to leave your feedback on the project**. Pedago Team really tries to make your educational experience better.
