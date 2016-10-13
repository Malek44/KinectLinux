KinectLinux
===========

We are going to install Libfreenect in order to stream real time depth video inside the Raspberry Pi.


Install Python-OpenCV and their dependencies:

First, update the package index:

    sudo apt-get update
    
It is also wise to upgrade the packages:
    
    sudo apt-get upgrade
    
If your linux distribution on Raspberry Pi is not the latest version, upgrade using:
    
    sudo apt-get dist-upgrade

Then, install OpenCV for Python and dependencies by typing the following commands:

    sudo apt-get install build-essential python-dev ipython python-opencv

    sudo apt-get install python-numpy python-scipy

    sudo apt-get install git-core git

Install dependencies for Libfreenect:

    sudo apt-get install freeglut3 freeglut3-dev libxmu-dev libxi-dev

    sudo apt-get install cmake cmake-curses-gui pkg-config

Install libusb 1.0.20 (latest version):

Now for libusb, the pre-compiled binary version 1.0.0 wont work with the Kinect. For that, you have to compile it and install it from source directly into your Raspberry Pi.

Install prerequisites:

    sudo apt-get install libudev-dev

Get the libusb source from github:

    sudo wget http://sourceforge.net/projects/libusb/files/libusb-1.0/libusb-1.0.20/libusb-1.0.20.tar.bz2/download

Decompress the content:

    tar xvjf download

Compile and install:

    cd libusb-1.0.20

    ./configure

    make

    sudo make install

Install Libfreenect:

Libfreenect is an opensource driver for Kinect on Linux machines. It interfaces to the Kinect and grab data from different sensors (IR images, RGB image, Depth Data). The source is available from github:

    cd ..

    git clone https://github.com/OpenKinect/libfreenect.git

    cd libfreenect

    mkdir build

    cd build

    ccmake ..

At this point, press ‘c’ key then with the arrow keys change BUILD EXAMPLES to OFF and make sure that LIBUSB_1_INCLUDE_DIR directory points to  /usr/local/include/libusb-1.0

Once done press ‘c’ again then ‘g’.

then enter the following command:

    cmake ..

    make

    sudo make install

Here you are done with installing libfreenect, so let test it.

Testing libfreenect with Python:

change your current directory to libfreenect/wrappers/python:

    cd ../wrappers/python

Then install the python module of libfreenect by typing:

    sudo python setup.py install

If everything is going ok you should now be able to test some demo applications:

    sudo python demo_cv_async.py

If your Kinect is unidentified or not found, check using "cheese" if it is working. If cheese works, and sudo python demo_cv_async.py does not, test this demo application instead:

    sudo python demo_cv2_async.py

As you may notice, the kinect pushes the Raspberry Pi 1 and 2 to its limits. The frame rate is clearly slower than that of modern desktop computers. However, this is easily understood by the fact that the Raspberry Pi is a small computer intended for small tasks with its 700MHz single core processor and the 512MB of RAM.

Using Raspberry Pi 3 Model B gives a much better frame rate, because it has 1GB RAM. The 64-bit Broadcom BCM2837 ARM v8 processor is a quad-core chip that runs at 1.2GHz, makes its performance comparable to an old desktop computer.

Always exit the program by Ctrl + C, otherwise the application would not have a clean exit and would need to be killed through the PID.
