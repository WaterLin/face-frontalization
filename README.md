# Face Frontalization
This is a Python port of the Face Frontalization code provided by Hassner *et al.* at http://www.openu.ac.il/home/hassner/projects/frontalize

The original code was written in Matlab and was ported to Python using Numpy and OpenCV.

![alt tag](https://raw.githubusercontent.com/dougsouza/face-frontalization/master/example.png)

### Dependencies
[Dlib Python Wraper](http://dlib.net) >= 18.17

[OpenCV Python Wraper](http://opencv.org/downloads.html) = 3.0.0

[SciPy](http://www.scipy.org/install.html)


- Windows x64: I have provided compiled binaries for OpenCV 3.0.0 and Dlib 18.18 [here](https://drive.google.com/file/d/0B7pvh2tbCWLLdElLYURTODdZSzg/view?usp=sharing). Just drag the files to your python packages folder (e.g. site-packages). If they don't work, you'll have to compile them yourself.
- Linux/OSX: You'll have to compile OpenCV and Dlib yourself.

### Other Dependencies
To run demo.py you must have:

[Matplotlib](http://matplotlib.org/)

### Citation
If you find this code useful please cite:

Tal Hassner, Shai Harel, Eran Paz and Roee Enbar, *Effective Face Frontalization in Unconstrained Images*, IEEE Conf. on Computer Vision and Pattern Recognition (CVPR), Boston, June 2015

# fix problem

Right now this code can run under this environment:

python 3.6.3
OpenCV 3.3.1

If you want to run this code under this environment, you should do following things:

## OpenCV 3.3.1 code

If you get following code error:

> Number of faces detected: 1
Backend MacOSX is interactive backend. Turning interactive mode on.
query image shape: (250, 250, 3)
OpenCV Error: Assertion failed (dst.cols < SHRT_MAX && dst.rows < SHRT_MAX && src.cols < SHRT_MAX && src.rows < SHRT_MAX) in remap, file /tmp/opencv-20170825-90583-1pdhamg/opencv-3.3.0/modules/imgproc/src/imgwarp.cpp, line 4944
Traceback (most recent call last):
  File "/Applications/PyCharm.app/Contents/helpers/pydev/pydevd.py", line 1585, in <module>
    globals = debugger.run(setup['file'], None, None, is_module)
  File "/Applications/PyCharm.app/Contents/helpers/pydev/pydevd.py", line 1015, in run
    pydev_imports.execfile(file, globals, locals)  # execute the script
  File "/Applications/PyCharm.app/Contents/helpers/pydev/_pydev_imps/_pydev_execfile.py", line 18, in execfile
    exec(compile(contents+"\n", file, 'exec'), glob, loc)
  File "/Users/farmer/code/face-frontalization/demo.py", line 49, in <module>
    demo()
  File "/Users/farmer/code/face-frontalization/demo.py", line 38, in demo
    frontal_raw, frontal_sym = frontalize.frontalize(img, proj_matrix, model3D.ref_U, eyemask)
  File "/Users/farmer/code/face-frontalization/frontalize.py", line 57, in frontalize
    frontal_raw[ind_frontal, :] = cv2.remap(img, temp_proj2[0, :].astype('float32'), temp_proj2[1, :].astype('float32'), cv2.INTER_CUBIC)
cv2.error: /tmp/opencv-20170825-90583-1pdhamg/opencv-3.3.0/modules/imgproc/src/imgwarp.cpp:4944: error: (-215) dst.cols < SHRT_MAX && dst.rows < SHRT_MAX && src.cols < SHRT_MAX && src.rows < SHRT_MAX in function remap

To fix this problem, just modify opencv-3.3.0/modules/imgproc/src/imgwarp.cpp, find this line of code and comment it out:

'CV_Assert( dst.cols < SHRT_MAX && dst.rows < SHRT_MAX && src.cols < SHRT_MAX && src.rows < SHRT_MAX );'

Recompile the OpenCV library and reinstall it.