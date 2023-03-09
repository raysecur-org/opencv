## OpenCV: Open Source Computer Vision Library

### Description
* Homepage: <https://opencv.org>

This version of OpenCV contains a patch that allows legacy USBv4 descriptor cameras to be used with the DirectShow backend.
Specifically, it changes the cap_dshow.cpp file so that it recognizes and handles USBv4's RGB565 pixel format exactly like USBv6's Y16 pixel format.
This allows using OpenCV to grab from both camera descriptors without any other specifics.
See [this ticket](https://ray-secur.atlassian.net/browse/RAYS-56) for more information.

### Building

WINDOWS 
1. Clone this repository to the desired filesystem location.  The correct branch to be cloned is release/4.1.x which can be cloned directly using command : 
```
git clone https://github.com/raysecur-org/opencv.git --branch release/4.1.x --single-branch
```
2. Create a "build" subfolder in the cloned directory
3. Start cmake-gui and click "Browse Source..." and select the opencv clone directory
4. Click "Browse Build" and select the build subfolder created at step 2.
5. Click "Configure", select "Visual Studio 16 2019" as Generator and "x64" as platform, then click "Finish" and wait for CMake to detect the configuration
6. Use the Search box to find and set the following entries to the correct value :
```  
  BUILD_PROTOBUF to FALSE
  WITH_PROTOBUF to FALSE
  BUILD_opencv_python3 to FALSE
  BUILD_opencv_python_bindings_generator to FALSE
  BUILD_opencv_world to TRUE  
```
7. Hit "Generate" to generate the build files, and then hit "Open Project" if you want to open it using Visual Studio
8. Build the INSTALL target in RELEASE configuration.  This will install OpenCV in the ./build/install directory where OpenCV is located
9. Switch to Debug configuration and build the INSTALL target again.  This will install debug dlls (postfixed with d in the filename) in the ./build/install directory as well

  LINUX :
  On linux, OpenCV is built and directly installed system-wide.

- Install some opencv dependencies
  ```
  > sudo apt install libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libavresample-dev
  > sudo apt install libcanberra-gtk-module ffmpeg
  ```
  Then clone and build OpenCV
  ```
  > git clone https://github.com/raysecur-org/opencv.git
  > cd opencv
  > git checkout release/4.1.x
  > mkdir build && cd build
  > sudo apt install pkg-config
  > cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_PROTOBUF=false -D WITH_PROTOBUF=false -D BUILD_opencv_python3=false -D BUILD_opencv_python_bindings_generator=false -D BUILD_opencv_world=true ..
  > make -j7
  > sudo make install
```

