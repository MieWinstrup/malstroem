malstroem
=========
Tools for screening of bluespots and water flow between bluespots

Features
--------
malstroem provides command line tools and a python api to calculate:

* Depressionless (filled, hydrologically conditioned) terrain models
* Surface flow directions
* Accumulated flow
* Blue spots
* Local watershed for each bluespot
* Pour points (point where water leaves blue spot when it is filled to its maximum capacity)
* Flow paths between blue spots
* Fill volume at specified rain incidents
* Spill over between blue spots at specified rain incidents

Assumptions
-----------
malstroem makes some assumptions to simplify calculations. The most important ones which you must be aware of:

* malstroem assumes that the terrain is an impermeable surface. This may change in a later version.
* malstroem does not know the concept of time. This means that the capacity of surface streams is infinite no matter the
width or depth. Streams wont flow over. The end result is the situation after infinite time, when all water has reached
its final destination.
* Water flows from one cell to one other cell (the D8 method).

Example usage
-------------
Calculate all derived data for 10mm and 30mm rain incidents ignoring bluespots where the maximum water depth is less than 5cm:

```bash
malstroem complete -r 10 -r 30 -filter 'maxdepth > 0.5' -dem dem.tif -outdir c:\outputdirectory
```


Installation
------------

Theoretically:

```bash
pip install cython numpy scipy gdal
pip install git+https://github.com/Kortforsyningen/malstroem.git[speedups]
```

Unfortunately the above doesn't work on all platforms as malstroem uses som third party libraries and has some optimized code which needs to be compiled for each platform. This method should work on most linux distributions.

### Installing on Windows

These instructions are for Python v2.7 64bit. Change accordingly if you prefer another version of Python.

 1. [Download](https://www.python.org/downloads/windows/) and install latest Python 2.7 "Windows x86-64 MSI installer" 
 2. [Download](http://aka.ms/vcpython27) and install "Microsoft Visual C++ Compiler for Python 2.7"
 3. Go to [Christoph Gohlke](http://www.lfd.uci.edu/~gohlke/pythonlibs/) and download `numpy`, `gdal`, `cython` and `scipy` wheels matching your python. For Python 2.7 64 bit it should be files ending in `cp27‑cp27m‑win_amd64.whl`
 4. Open windows command prompt and go to the scripts folder in your Python installation. In a defaut install it should be something like
  ```
  cd c:\Python27\scripts
  ```
 5. For each of the 4 wheel files downloaded from Gholke (starting with `numpy`) install it with pip like this:
 ```
 pip install c:\downloads\numpy‑1.11.3+mkl‑cp27‑cp27m‑win_amd64.whl
 ```
 6. Clone malstroem from github
 ```
 git clone https://github.com/Kortforsyningen/malstroem
 ```
 7. Now (finally) install malstroem
 ```
 pip install c:\downloads\malstroem[speedups]
 ```
 8. Still in the scripts folder of your Python (c:\python27\scripts) check that malstroem responds to
 ```
 malstroem --help
 ```
 
### Installing on Mac OSX
 The biggest problem on OSX is getting GDAL to work. One known solution is via [homebrew](http://brew.sh/)
 1. Make sure homebrew is installed and you know how to use its Python (See for instance [this guide](http://docs.python-guide.org/en/latest/starting/install/osx/))
 2. Install GDAL and its Python bindings
 
  ```
  brew install gdal
  ```
 3. Make sure you use the homebrew Python and install malstroem and its dependencies (If you are using a virtualenv create       it using `--system-site-packages`) 
 
  ```
  pip install cython numpy scipy
  pip install git+https://github.com/Kortforsyningen/malstroem.git[speedups]
  ```

Bugs and contributions
----------------------
- Please report issues using the issue tracker: github.com/Kortforsyningen/malstroem/issues
- Contributions are welcome at github.com/Kortforsyningen/malstroem/

If you are not familiar with GitHub please read this short [guide](https://guides.github.com/activities/contributing-to-open-source/).

License
-------
```
Copyright (c) 2016
Developed by Septima.dk and Thomas Balstrøm (University of Copenhagen) for the Danish Agency for
Data Supply and Efficiency. This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by the Free Software Foundation,
either version 2 of the License, or (at you option) any later version.
This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without
even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PORPOSE. See the GNU Gene-
ral Public License for more details.
You should have received a copy of the GNU General Public License along with this program. If not,
see http://www.gnu.org/licenses/.
```
