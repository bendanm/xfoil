# Fork of XFOIL
## About
*Subsonic Airfoil Development System*

<http://web.mit.edu/drela/Public/web/xfoil/>

A copy of [RobotLocomotion/xfoil](https://github.com/RobotLocomotion/xfoil)
with further instructions for building for MacOSX. 

## General Unix Installation

```
$ mkdir build && cd build
$ cmake ..
$ make install
```

## MacOSX Installation 

Install Homebrew from https://brew.sh/ by running the following command in the 
Terminal.app:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Open Terminal.app and run the following to the intall pre-requisites:

```
brew update && brew cask install xquartz && brew install cmake gcc; 
```

Download and build xfoil:

```
mkdir xfoil && cd xfoil && curl -L -k https://github.com/bendanm/xfoil/tarball/master | tar --strip-components=1 -zx && mkdir build && cd build && cmake .. && make install ;
```

The above snippit:
1. Makes a directory called xfoil to download the code into
2. Downloads and extracts [xfoil](https://github.com/bendanm/xfoil/) to directory
3. Builds xfoil from source and installs to default location, by default `/usr/local/bin`
4. The xfoil directory that the source code was downloaded into can be deleted when complete. 

### MacOSX Notes

#### Restart after XQuartz installation

If XQuartz was newly installed, restart your computer so that the DISPLAY 
enviroment variable will be correctly inialised before launching xfoil. See the 
[XQuartz documentation](https://www.xquartz.org/releases/XQuartz-2.7.11.html) 
for more information. 

#### Run XQuartz in background

Before running xfoil from Termainal, make sure XQuartz is running in the 
background:

```
~ $ open -a XQuartz.app
~ $ xfoil file.dat
```

#### Known error - IO error 35

If the Xplot11 window is closed, xfoil will keep trying to draw to the same 
window and crash with:

```
XIO:  fatal IO error 35 (Resource temporarily unavailable) on X server
```

Do not close the Xplot11 XQuartz window until you are finished. 