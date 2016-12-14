
**bv** is a small tool to quickly view high-resolution multi-band imagery
directly in your [iTerm 2](https://www.iterm2.com). It was designed for
visualising very large images located on a remote machine over a low-bandwidth
connection. It subsamples and compresses the image and then sends over the wire
as a PNG that has been base64 encoded (hence the name "bv") that iTerm 2 then 
inlines in your terminal.

<img src="https://github.com/daleroberts/bv/raw/master/docs/trump.png" width="800">

Now, go and compare the above to [old-school rendering](https://camo.githubusercontent.com/a6c791a0b4d97315d00b6592f918fe744abe00e6/687474703a2f2f692e696d6775722e636f6d2f556e666e704d722e706e67)
or my other tool [tv](https://github.com/daleroberts/tv). Welcome to 2017!

# Examples

Here are a number of examples that show how this tool can be used.

## Big image over small connection

Display a 3.5 billion pixel single-band image (3.3GB) using only 467KB over a SSH connection.

<img src="https://github.com/daleroberts/bv/raw/master/docs/bigimg.png" width="800">

## Different band combinations

Display a six-band image (7.2GB) using only 1.1MB over a SSH connection. Here,
we put bands 5-4-3 into the RGB channels using `-b 5 -b 4 -b 3` and set the
width of the output image to be 600 pixels using `-w 600`.

<img src="https://github.com/daleroberts/bv/raw/master/docs/bands.png" width="800">



## Machine learning classifier output with different color maps

Different color maps can be applied to single-band images using the `-cm`
option and any choice from [matplotlib's
colormaps](http://matplotlib.org/examples/color/colormaps_reference.html). The
width (in pixels) of the output image can also be specified with the `-w`
option.

<img src="https://github.com/daleroberts/bv/raw/master/docs/colors.png" width="800">

# Installation

It is just a single-file script so all you'll need to do it put it in your
`PATH`. Dependencies are Python 3, GDAL 2, Numpy, Matplotlib, and iTerm 2. I've
found that the best way to install these dependencies are: 
```bash
# Python 3
brew install python3

# Numpy and matplotlib
pip3 install numpy matplotlib

# GDAL 2
brew install gdal --HEAD --without-python
pip3 install gdal
```
