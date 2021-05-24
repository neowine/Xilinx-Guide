문제
---
```log
CMake Error at CMakeLists.txt:23 (find_package):
  By not providing "FindOpenCV.cmake" in CMAKE_MODULE_PATH this project has
  asked CMake to find a package configuration file provided by "OpenCV", but
  CMake did not find one.

  Could not find a package configuration file provided by "OpenCV" with any
  of the following names:

    OpenCVConfig.cmake
    opencv-config.cmake

  Add the installation prefix of "OpenCV" to CMAKE_PREFIX_PATH or set
  "OpenCV_DIR" to a directory containing one of the above files.  If "OpenCV"
  provides a separate development package or SDK, be sure it has been
  installed.


-- Configuring incomplete, errors occurred!
See also "/home/nw2/vitis_in_depth_tutorial/Vitis-Tutorials/Hardware_Accelerators/Design_Tutorials/03-rtl_stream_kernel_integration/sw/build/CMakeFiles/CMakeOutput.log".

```

OpenCV 패키지가 없어서 발생하는 문제


해결방법
---
```bash
sudo apt-get install libopencv-dev
```
