FaceAlign
====
FaceAlign is a tool that can be used to align a set of images containing faces.
It is particularly useful for creating time-lapse face videos, such as [this one](http://youtube.com/watch?v=7SXErQ4eYGU).

How it works
----
FaceAlign is a Python script that uses [OpenCV python bindings](http://OpenCV.willowgarage.com/wiki/) (which requires >= Python 2.6).
It detects the location of the face in each image (OpenCV tends to err on the side of over-detection, and this tool will use the largest detected face) and will scale and offset the image so that the centers of the faces in all images match up.
This is based on parameters that can be easily set in [config.py](src/config.py).

On OS X, OpenCV can be installed with [homebrew](http://brew.sh).
To do so, install homebrew and run the following command in your terminal.

    $  brew install OpenCV --32-bit
    
Usage
----
Once Python and [OpenCV](http://OpenCV.org) are installed, open [config.py](src/config.py) and set HCDIR to the folder containing your OpenCV installation's Haar cascade files.

On OS X, you can find the Haar cascade files under `/usr/local/Cellar/OpenCV/2.4.9/share/OpenCV/haarcascades` if you've used homebrew to install OpenCV.

Run sizeToFace.py.
It takes a required input directory parameter, and an optional output directory parameter.
The output directory will be created if it does not already exist.
By default, images will be output to the current directory.
Output file names will be numbered starting with 0001.jpg.

    $ python src/sizeToFace.py ../in-images
    $ python src/sizeToFace.py ../in-images ../out-images

Eventual plans
----
* Brightness/contrast normalization
* Integration with ffmpeg for automatic video generation
* A GUI

Common Errors/Solutions
----
    ImportError: No module named cv

**Solution**: You have not installed OpenCV or the OpenCV Python bindings.

    Traceback (most recent call last):
     File "<...>/src/facealign/src/FaceImage.py", line 133, in runFaceImage
       fi.cropToFace()
     File "<...>/src/facealign/src/FaceImage.py", line 23, in cropToFace
       face = self._getFaceCoords()
     File "<...>/src/facealign/src/FaceImage.py", line 68, in _getFaceCoords
       cascade = cv.Load(HCPATH)
    TypeError: OpenCV returned NULL

**Solution**: This means you have not set your HCDIR variable correctly.
*Open src/config.py and set HCDIR to
[yourOpenCVDir]/OpenCV/data/haarcascades/, for example:
HCDIR = '/home/doriad/src/OpenCV/OpenCV/data/haarcascades/'

So what's up?
----
Feedback, ideas, issue reports, and contributions are invited.
Welcomed.
Demanded, even.
FaceAlign is fairly simple at the moment but I would be interested to hear if you found it useful. 
