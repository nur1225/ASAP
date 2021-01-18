# ASAP - Automated Slide Analysis Platform

[![Build status](https://ci.appveyor.com/api/projects/status/gy0rv4vos88aiq53?svg=true)](https://ci.appveyor.com/project/GeertLitjens/asap)

ASAP is an open source platform for visualizing, annotating and automatically analyzing whole-slide histopathology images. It consists of several key-components (slide input/output, image processing, viewer) which can be used seperately. It is built on top of several well-developed open source packages like OpenSlide, Qt and OpenCV but also tries to extend them in several meaningful ways.

#### Features

- Reading of scanned whole-slide images from several different vendors (Aperio, Ventana, Hamamatsu, Olympus, support for fluorescence images in Leica LIF format)
- Writing of generic multi-resolution tiled TIFF files for ARGB, RGB, Indexed and monochrome images (including support for different data types like float)
- Python wrapping of the IO library for access to multi-resolution images through Numpy array's
- Basic image primitives (Patch) which can be fed to image processing filters, connection to OpenCV
- Qt-based viewer to visualize whole-slide images in a fast, fluid manner
- Point, polygonal and spline annotation tools to allow annotation of whole slide images.
- Annotation storage in simple, human-readable XML for easy use in other software
- Viewer and reading library can easily be extended by implementing plugins using one of the four interface (tools, filters, extensions, fileformats)
- Integration of on-the-fly image processing while viewing (current examples include color deconvolution and nuclei detection)

#### Installation

Currently ASAP is only supported under 64-bit Windows and Linux machines. Compilation on other architectures should be relatively straightforward as no OS-specific libraries or headers are used. The easiest way to install the software is to download the binary installer or .DEB package from the release page. **If you install the DEB package, you can find the ASAP executable under /opt/ASAP/bin**.

#### Compilation

To compile the code yourself, some prerequesites are required. First, we use CMake (version >= 3.5) as our build system and Microsoft Visual Studio or GCC as the compiler. The software depends on numerous third-party libraries:

- Boost (http://www.boost.org/)
- OpenCV (http://www.opencv.org/)
- Qt (http://www.qt.io/)
- libtiff (http://www.libtiff.org/)
- libjpeg (http://libjpeg.sourceforge.net/)
- JasPer (http://www.ece.uvic.ca/~frodo/jasper/)
- DCMTK (http://dicom.offis.de/dcmtk.php.en)
- SWIG (http://www.swig.org/) (only for Python wrapping of the IO library)
- OpenSlide (http://openslide.org/)
- PugiXML (http://pugixml.org/)
- zlib (http://www.zlib.net/)
- unittest++ (https://github.com/unittest-cpp/unittest-cpp)

To help developers compile this software themselves we provide the necesarry binaries (Visual Studio 2013, 64-bit) for all third party libraries on Windows except Boost, OpenCV and Qt (due to size constraints). See the Release page for binaries. If you want to provide the packages yourself, there are no are no strict version requirements, except for libtiff (4.0.1 and higher), Boost (1.55 or higher), Qt (5.1 or higher) and OpenCV (3.1). On Linux all packages can be installed through the package manager on Ubuntu-derived systems (tested on Ubuntu and Kubuntu 18.04 LTS). You can also use the provided Dockerfile for Linux builds (under buildtools).

Subsequently, fire up CMake, point it to a source and build directory and hit Configure. Select your compiler of preference and hit ok. This will start the iterative process of CMake trying to find a third party dependency and you specifiying its location. The first one to provide will be Boost. To allow CMake to find Boost add a BOOST\_ROOT variable pointing to for example C:/libs/boost\_1\_57\_0. Then press Configure again and CMake will ask for the next library. These should be pretty straightforward to fill in (e.g. TIFF\_LIBRRARY should point to tiff.lib, TIFF\_INCLUDE\_DIRECTORY to |folder to libtiff|\include. If more steps are unclear, please open a ticket on the Github issue-tracker.

During configuration you will notice that several parts of ASAP can be built seperately (e.g. the viewer). To build this part, simply check the component and hit Configure again. The 'Package on install'-option will allow you to build a binary setup-package like the one provided on the Github-release page. On Windows this requires NSIS to be installed.

After all the dependencies are resolved, hit Generate and CMake will create a Visual Studio Solution or makefile file which can be used to compile the source code.
## ASAP 源码编译 VS2019
# 安装 ASAP 依赖包
- Boost (http://www.boost.org/)
  -下载 boost源码并解压
  -打开cmd 并 cd boost 根目录
  -运行 bootstrap.bat 文件生成 b2.exe 可执行文件 ： cd boost , bootstrap.bat
  -运行b2.exe 文件 生成 lib文件夹下和include 文件夹下的头文件 ： b2.exe toolset=msvc-14.2 --build-type=complete architecture=x86 address-model=64 link=static variant=debug,release threading=multi runtime-link=static instal
  -C盘中生成 Boost 文件夹
- OpenCV (http://www.opencv.org/)
- Qt (http://www.qt.io/)
- DCMTK-LIBJPEG (链接：https://pan.baidu.com/s/1dA28UIwFy2hIuONv11Y6pw )【密码：1234】
-- 下载百度网盘中DCMTK 文件夹并解压即可
- SWIG (http://www.swig.org/) (only for Python wrapping of the IO library)
-- 官方中下载并安装即可
- OpenSlide (链接：https://pan.baidu.com/s/12h2cJOyvqH6-3ekj5FXabw)   【密码：1234】
-- 下载百度网盘中OpenSlide 文件夹并解压即可
- PugiXML (http://pugixml.org/)
-- 官方中下载PuguiXML 并安装即可

## ASAP源码进行Cmake
- cmake -B ./build -DBOOST_ROOT=C:\Boost -DJPEG_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/include  -DJPEG_LIBRARY_DEBUG=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libjpeg.dll.a  -DJPEG_LIBRARY_RELEASE=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libjpeg.dll.a -DOpenJPEG_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/openjpeg-2.3 -DOPENSLIDE_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/include/openslide -DOPENSLIDE_LIBRARY=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/lib/libopenslide.lib -DDCMTKJPEG_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/include -DDCMTKJPEG_LIBRARY=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/lib/ijg8.lib -DTIFF_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/include -DTIFF_LIBRARY_DEBUG=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libtiff.dll.a -DTIFF_LIBRARY_RELEASE=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libtiff.dll.a -DZLIB_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/include -DZLIB_LIBRARY_DEBUG=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libz.dll.a -DZLIB_LIBRARY_RELEASE=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libz.dll.a -DPugiXML_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/pugixml/src -DBUILD_MULTIRESOLUTIONIMAGEINTERFACE_VSI_SUPPORT=ON -DPACKAGE_ON_INSTALL=TRUE -DBUILD_ASAP=TRUE -DBUILD_IMAGEPROCESSING=TRUE -DBUILD_EXECUTABLES=TRUE -DQt5_DIR=C:/Qt/Qt5.9.2/5.9.2/msvc2017_64/lib/cmake/Qt5 -DOpenCV_DIR=C:/opencv-4.3.0/opencv/build/x64/vc14/lib -DBUILD_WORKLIST_INTERFACE=TRUE -DWRAP_MULTIRESOLUTIONIMAGEINTERFACE_PYTHON=ON -DWRAP_WHOLESLIDEFILTERS_PYTHON=ON -DPYTHON_DEBUG_LIBRARY=D:/tools/conda/envs/asap/libs/python38.lib -DPYTHON_LIBRARY=D:/tools/conda/envs/asap/libs/python38.lib -DPYTHON_LIBRARY_DEBUG=D:/tools/conda/envs/asap/libs/python38.lib -DPYTHON_INCLUDE_DIR=D:/tools/conda/envs/asap/include -DPYTHON_EXECUTABLE=D:/tools/conda/envs/asap/python.exe -DPYTHON_NUMPY_INCLUDE_DIR=D:/tools/conda/envs/asap/Lib/site-packages/numpy/core/include -DDCMTKJPEG_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/include -DDCMTKJPEG_LIBRARY=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/lib/ijg8.lib -DSWIG_EXECUTABLE=D:/workspace/srcCode/ASAP-1.9/thirdpart/swigwin-4.0.1/swig.exe
- cd build
- cmake --build . --config Release
- cpack 
- mv ASAP-1.9-win64.exe $env:artefact_name  【可选】

# 参数介绍
- cmake -B ./build 
-DBOOST_ROOT=C:\Boost             
-DJPEG_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/include  
-DJPEG_LIBRARY_DEBUG=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libjpeg.dll.a  
-DJPEG_LIBRARY_RELEASE=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libjpeg.dll.a 
-DOpenJPEG_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/openjpeg-2.3 
-DOPENSLIDE_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/include/openslide 
-DOPENSLIDE_LIBRARY=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/lib/libopenslide.lib 
-DDCMTKJPEG_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/include 
-DDCMTKJPEG_LIBRARY=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/lib/ijg8.lib 
-DTIFF_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/include 
-DTIFF_LIBRARY_DEBUG=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libtiff.dll.a 
-DTIFF_LIBRARY_RELEASE=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libtiff.dll.a 
-DZLIB_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/include 
-DZLIB_LIBRARY_DEBUG=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libz.dll.a 
-DZLIB_LIBRARY_RELEASE=D:/workspace/srcCode/ASAP-1.9/thirdpart/custom_openslide/artefacts/lib/libz.dll.a 
-DPugiXML_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/pugixml/src 
-DBUILD_MULTIRESOLUTIONIMAGEINTERFACE_VSI_SUPPORT=ON 
-DPACKAGE_ON_INSTALL=TRUE 
-DBUILD_ASAP=TRUE 
-DBUILD_IMAGEPROCESSING=TRUE 
-DBUILD_EXECUTABLES=TRUE 
-DQt5_DIR=C:/Qt/Qt5.9.2/5.9.2/msvc2017_64/lib/cmake/Qt5 
-DOpenCV_DIR=C:/opencv-4.3.0/opencv/build/x64/vc14/lib 
-DBUILD_WORKLIST_INTERFACE=TRUE 
-DWRAP_MULTIRESOLUTIONIMAGEINTERFACE_PYTHON=ON 
-DWRAP_WHOLESLIDEFILTERS_PYTHON=ON 
-DPYTHON_DEBUG_LIBRARY=D:/tools/conda/envs/asap/libs/python38.lib 
-DPYTHON_LIBRARY=D:/tools/conda/envs/asap/libs/python38.lib 
-DPYTHON_LIBRARY_DEBUG=D:/tools/conda/envs/asap/libs/python38.lib 
-DPYTHON_INCLUDE_DIR=D:/tools/conda/envs/asap/include 
-DPYTHON_EXECUTABLE=D:/tools/conda/envs/asap/python.exe 
-DPYTHON_NUMPY_INCLUDE_DIR=D:/tools/conda/envs/asap/Lib/site-packages/numpy/core/include 
-DDCMTKJPEG_INCLUDE_DIR=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/include 
-DDCMTKJPEG_LIBRARY=D:/workspace/srcCode/ASAP-1.9/thirdpart/dcmtk-libjpeg/lib/ijg8.lib 
-DSWIG_EXECUTABLE=D:/workspace/srcCode/ASAP-1.9/thirdpart/swigwin-4.0.1/swig.exe

如果在运行这步系统报错主要（boost 依赖包安装有问题，重新安装boost，PugiXML 依赖包安装出现问题，重新安装【因为找不到boost 和 PugiXML文件夹中有些文件】）
# cmake --build . --config Release
如果ASAP编译到这步报错主要是 python 安装包出现问题，请重新查看第一步中python 的路径是否正确，并numpy 是否安装...

# cpack 
如果ASAP编译到这步报错主要是 cpack的有些依赖包没安装，cpack 依赖包安装即可 【找不到 NSIS软件 (https://sourceforge.net/projects/nsis/) ，下载安装该软件即可】

# mv ASAP-1.9-win64.exe $env:artefact_name
如果ASAP编译到这步报错主要是CMD中mv不是内部或外部命令....... 
