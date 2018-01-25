# teaching-vision
This project provides the exercises for my visual computing class in which the students are ought to solve various tasks that are closely related to the course material.

## setup
I highly recommend using Anaconda with Python 3 to do the exercises. You can obtain the version that I will be using by executing the following commands. Feel free to use other environments as well. However, the recommended environment is what will be used for grading. Furthermore, while you are encouraged to use your own machine, please note that I am unable to provide individual support.

```bash
wget https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh
bash Anaconda3-4.2.0-Linux-x86_64.sh -b -p $HOME/anaconda
rm Anaconda3-4.2.0-Linux-x86_64.sh
export PATH="$HOME/anaconda/bin:$PATH"
conda install -y -c menpo opencv3
```

Should you be using the machines in the Linux lab, you also need to make sure that you run the `export` command again when logging out and back in. Since the Linux lab is a shared environment, the `.bashrc` cannot be modified which prevents Anaconda from doing this automatically for you.

## `01-colorspace` (5 points)
Follow the description in "Color Transfer between Images" by Reinhard et al. to convert an image to the LMS color space. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.stack.html

Notice that the resulting image will show the LMS color space as an RGB color space, which has little meaning.

## `02-colortransfer` (5 points)
Follow the description in "Color Transfer between Images" by Reinhard et al. to match the color distribution of one image to another. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.ndarray.mean.html
* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.ndarray.std.html

Feel free to try this out on images of your own. You may find that the resulting quality varies and that some examples work better than others.

## `03-demosaicing` (10 points)
Implement the bilinear interpolation described in the slides as well as in "Interactions Between Color Plane Interpolation and Other Image Processing Functions in Electronic Photography" by Adams to perform demosaicing of Bayer patterns. Some resources that can potentially help you to achieve this goal are stated blow.

* http://python-reference.readthedocs.io/en/latest/docs/operators/modulus.html
* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.ndarray.shape.html

Notice that diagonal edges are particularly prone to artifacts with this simple approach. In partice, other algorithms work much better.

## `04-convolution` (5 points)
Use convolutions to implement demosaicing algorithm described in the slides as well as in "Interactions Between Color Plane Interpolation and Other Image Processing Functions in Electronic Photography" by Adams. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.opencv.org/3.4.0/d4/d86/group__imgproc__filter.html#ga27c049795ce870216ddfb366086b5a04

Other than that the output is one pixel larger on each side, the result should otherwise be identical to the previous exercise that does not make use of convolutions. The new approach is likely to be much faster though.

## `05-median` (5 points)
Filter a given image once by using a Gaussian kernel and once by using a median filter. Feel free to use the functions built into OpenCV which are implementaitons of the theory covered in class. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.opencv.org/3.4.0/d4/d86/group__imgproc__filter.html#gaabe8c836e97159a9193fb0b11ac52cf1
* https://docs.opencv.org/3.4.0/d4/d86/group__imgproc__filter.html#ga564869aa33e58769b4469101aac458f9

Notice that the [implementation](https://github.com/opencv/opencv/blob/master/modules/imgproc/src/smooth.cpp#L2686) of the median filtering is heavily optimized. Our usage of this implementation could potentially be sped up by using `uint8` over `float32` arrays.

## `06-spectrum` (10 points)
Make use of the convolution theorem and implement a convolution as a Hadamard product in the frequency space. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.pad.html
* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.roll.html
* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.fft.fft2.html
* https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.fft.ifft2.html

Make sure to examine the resulting plot of the spectrum and how the diagonal within the filter kernel is resembled in its frequency spectrum.

## `07-pyramid` (5 points)
Implement a Laplacian pyramid described in the slides as well as in "The Laplacian Pyramid as a Compact Image Code" by Burt and Adelson. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.opencv.org/3.4.0/d4/d86/group__imgproc__filter.html#gaf9bba239dfca11654cb7f50f889fc2ff
* https://docs.opencv.org/3.4.0/d4/d86/group__imgproc__filter.html#gada75b59bdaaca411ed6fee10085eb784

Due to the built-in `pyrDown` and `pyrUp` functions of OpenCV, this tasks becomes relatively simple since they directly mimic the `REDUCE` and `EXPAND` operations.

## `08-homography` (10 points)
Given four corresponding points, estimate the Homography matrix and warp the image accordingly. Do this step by step as shown in class and do not use the functions state below.

* https://docs.opencv.org/3.4.0/d9/d0c/group__calib3d.html#ga4abc2ece9fab9398f2e560d53c8c9780
* https://docs.opencv.org/3.4.0/da/d54/group__imgproc__transform.html#gaf73673a7e8e18ec6963e3774e6a94b87

Note that the approach without bilinear interpolation that I showed in class is fairly slow due to Python. A sampling grid could be used to speed this up.

## `09-colorize` (5 points)
Compose a color image from a [Prokudin-Gorskii](https://www.loc.gov/pictures/collection/prok/process.html) photo by aligning the invididual exposures and stacking them. Some resources that can potentially help you to achieve this goal are stated blow.

* https://docs.opencv.org/3.4.0/dc/d6b/group__video__track.html#ga7ded46f9a55c0364c92ccd2019d43e3a
* https://docs.opencv.org/3.4.0/da/d54/group__imgproc__transform.html#gaf73673a7e8e18ec6963e3774e6a94b87

Note that the movement of individual objects in between two exposures is not captured by the Homography transform. We will discuss how to address these in a different lecture.

## linux lab
When connecting remotely into the Linux lab, please choose one of the machines in the [first](https://cat.pdx.edu/labstatus/labs/cslinlaba/) or the [second](https://cat.pdx.edu/labstatus/labs/cslinlabb/) lab. After selecting a machine, you can use your credentials to establish a connection through ssh. Note that you can alternatively use PuTTY as well.

```
ssh <username>@<machine>.cs.pdx.edu
```

I am well aware that this is rather inconvenient but it is at least guaranteed to work. You are furthermore encouraged to use your own computer without connecting remotely into the Linux lab. However, I am unable to provide individual support to get the framework to run on your own computer.

## virtual machine
Using a virtual machine is always a viable option. I personally do this as well and developed these exercises in a Debian environment that is running within a virtual machine. Note that there are quite a few free virtualizers to choose from and while I have a preferred one, I would like to take the liberty of not making any advertisements here. Therefore, I would recommend reading a few related online resources.

## images
* blend by [Juliane Aulbach](https://www.linkedin.com/in/aulbach)
* demosaicing by [Patrick Vandewalle et al.](http://lcavwww.epfl.ch/reproducible_research/VandewalleKAS07)
* fusion, homography, panorama, and text by [Simon Niklaus](https://www.linkedin.com/in/sniklaus)
* fruits by [romanov](https://pixabay.com/en/fruits-sweet-fruit-exotic-82524/)
* multiband by [Peter J. Burt and Edward H. Adelson](http://dl.acm.org/citation.cfm?id=247)
* prokudin by [Sergey Prokudin-Gorsky](https://www.loc.gov/pictures/collection/prok/process.html)
* transfer by [Reinhard et al.](http://ieeexplore.ieee.org/document/946629)

## license
Please refer to the appropriate file within this repository.