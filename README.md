# Fork of XFOIL
## About
*Subsonic Airfoil Development System*

<http://web.mit.edu/drela/Public/web/xfoil/>

A copy of [RobotLocomotion/xfoil](https://github.com/RobotLocomotion/xfoil)
with further instructions for building for MacOSX. 

## General Unix Installation steps

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
