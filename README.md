
**bv** is a small tool to quickly view high-resolution multi-band imagery
directly in your [iTerm 2](https://www.iterm2.com). It was designed for
visualising very large images located on a remote machine over a low-bandwidth
connection. It subsamples and compresses the image and then sends over the wire
as a PNG that has been base64 encoded (hence the name "bv").

<img src="https://github.com/daleroberts/bv/raw/master/docs/trump.png" width="800">

# Installation

It is just a single-file script so all you'll need to do it put it in your
`PATH`. Dependencies are Python 3, GDAL 2, Numpy, and iTerm 2. I've found that
the best way to install these dependencies are: 
```bash
# Python 3
brew install python3

# Numpy
pip3 install numpy

# GDAL 2
brew install gdal --HEAD --without-python
pip3 install gdal
```
