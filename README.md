
**bv** is a small tool to quickly view high-resolution multi-band imagery
directly in your [iTerm 2](https://www.iterm2.com). It was designed for
visualising very large images located on a remote machine over a low-bandwidth
connection. It subsamples and compresses the image sends it over the wire as a
base64-encoded PNG (hence the name "bv") that iTerm 2 inlines in your terminal.

<img src="https://github.com/daleroberts/bv/raw/master/docs/trump.png" width="800">

Now, go and compare the above to [old-school rendering](https://camo.githubusercontent.com/a6c791a0b4d97315d00b6592f918fe744abe00e6/687474703a2f2f692e696d6775722e636f6d2f556e666e704d722e706e67)
or my other tool [tv](https://github.com/daleroberts/tv). Welcome to 2017!

# Some Examples

Here are a number of examples that show how this tool can be used.

## Big image over small connection

Display a 3.5 billion pixel single-band image (3.3GB) using only 467KB over a SSH connection.

<img src="https://github.com/daleroberts/bv/raw/master/docs/bigimg.png" width="800">

## Different band combinations

Display a six-band image (7.2GB) using only 1.1MB over a SSH connection. Here,
we put bands 5-4-3 into the RGB channels using `-b 5 -b 4 -b 3` (ordering
matters) and set the width of the output image to be 600 pixels using `-w 600`.

<img src="https://github.com/daleroberts/bv/raw/master/docs/bands.png" width="800">

You can also specify a single band to display (e.g., `-b 1`).

## Subset images

You can subset images using `gdal_translate` syntax which is `-srcwin xoff yoff
xsize ysize`. For example, only displaying a small 1000x1000 area of the same large image above.

<img src="https://github.com/daleroberts/bv/raw/master/docs/subset.png" width="800">

This allows you to quickly identify regions of your image and then paste the same options 
into `gdal_translate` to complete your desired workflow. For example:
```
remote$ gdal_translate tasmania-2014.tif -b 5 -b 4 -b 3 -srcwin 12000 11000 1000 1000 -of PNG -ot UInt16 -scale 0 4000 ~/out.png
Input file size is 20000, 16000
0...10...20...30...40...50...60...70...80...90...100 - done.
remote$
```

## Machine learning multi-class outputs with different color maps

Sometimes you might have a single-band image that only contains classes
(integers). Different color maps can be applied to these single-band images
using the `-cm` option and any choice from [matplotlib's
colormaps](http://matplotlib.org/examples/color/colormaps_reference.html).

<img src="https://github.com/daleroberts/bv/raw/master/docs/colors.png" width="800">

## URLs

The **bv** tool can read from URLs (see the Trump image above). It can also
parse URLs on `stdin`, this allows you to [do
things](https://github.com/developmentseed/landsat-util) like this to quicky
display available Landsat images roughly over Dubai.

```
remote$ landsat search --lat 25 --lon 55 --latest 3 | bv -urls -
```

## Standard Input

Filenames can be read from `stdin`. For example:
```
ls -1 *.tif | bv -w 100 -
```

## Compression

The level of compression can be changed using the `-zlevel` option (0-9).

## Stacking images

If your bands are located in seperate images then you can stack them and display them
in the RGB channels using
```
bv -stack RED.tif GREEN.tif BLUE.tif
```

There is also the `-revstack` option to do it in reverse order.

## Subsampling algorithm

The subsampling algorithm can be changed using the `-r` option (same syntax as GDAL). The available subsamplings are:
- Nearest
- Average
- Cubic Spline
- Cubic
- Mode
- Lanczos
- Bilinear

## Alpha channel

For single-band images, you can specify the color value to set as the alpha
channel. This is sometimes useful for machine learning outputs where you want
to not display certain classes. You can add multiple of these with different
values.

## PDF, EPS, and PNG

The **bv** tool will display PDF, EPS, and PNG output inline with out any
changes to those files. If you want to disable this behaviour you can pass the
`-nop` option allow GDAL to subsample, etc.

## TMUX Support

<img src="https://github.com/daleroberts/bv/raw/master/docs/tmux.png" width="800">

# Configuration

You can save your default configuration by setting an alias in your `~/.profile` file. For example, I do:
```
alias bv='bv -w 800'
```

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
