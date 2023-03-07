## OpenCV: Open Source Computer Vision Library

### Description
* Homepage: <https://opencv.org>

This version of OpenCV contains a patch that allows legacy USBv4 descriptor cameras to be used with the DirectShow backend.
Specifically, it changes the cap_dshow.cpp file so that it recognizes and handles USBv4's RGB565 pixel format exactly like USBv6's Y16 pixel format.
This allows using OpenCV to grab from both camera descriptors without any other specifics.
See [this ticket](https://ray-secur.atlassian.net/browse/RAYS-56) for more information.

### Building

1. Clone this repository to the desired filesystem location
2. Create a "build" subfolder in the cloned directory
3. Use CMAKE to generate build files (either using cmake-gui or the commandline) for x64 with the following settings : 
  a. set BUILD_PROTOBUF to FALSE
  b. set WITH_PROTOBUF to FALSE
  c. set BUILD_opencv_python3 to FALSE
  d. set BUILD_opencv_python_bindings_generator to FALSE
  e. set BUILD_opencv_world to TRUE
  f. If using the CMake GUI, hit "Generate" to generate the build files, and then hit "Open Project"
4. Build the INSTALL target in RELEASE configuration.  This will install OpenCV in the ./build/install directory where OpenCV is located
5. Switch to Debug configuration and build the INSTALL target again.  This will install debug dlls (postfixed with d in the filename) in the ./build/install directory as well
