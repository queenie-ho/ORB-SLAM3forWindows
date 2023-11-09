# ORB-SLAM3 for Windows
This is just to archive the ORB-SLAM3 for Windows and the source code is from https://github.com/chanho-code/ORB-SLAM3forWindows

ORB-SLAM3 Project for Windows Platform (espacially Visual Studio)  
We have tested the library in Windows 10, Visual Studio 2015.

# Reference
- ORB-SLAM3 project: https://github.com/UZ-SLAMLab/ORB_SLAM3  
- ORB-SLAM2 for windows: https://github.com/Phylliida/orbslam-windows  
- ORB-SLAM2 for windows_2: https://github.com/phdsky/ORBSLAM24Windows  

# To do...
Update from ORB-SLAM3 V0.2 to V0.3


# Prerequisites

1. Visual Studio: Tested with VS2015

2. Cmake: Required at least 2.8. (Tested with 3.14.7)

3. OpenCV: Required at least 3.0. (Tested with 3.4.1)

4. glew (for pangolin): Tested with 2.1.0

5. boost: Tested with 1.67.0: https://www.boost.org/users/history/version_1_67_0.html  

# Build
## eigen  

## DBoW2  
- Open cmake-gui and make a 'build' directory in ORB-SLAM3forWindows/Thirdparty/DBoW2  
- Click Configure and select Visual Studio 14 2015 x64.  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- Right click on DBoW2 project -> Properties -> General -> Target Extension: .lib, and Configure Type: Static Library (.lib)  
- DBoW2 project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- Build ALL_BUILD. Finish(DBoW2.lib).

## g2o  
- Open cmake-gui and Make a 'build' directory in ORB-SLAM3forWindows/Thirdparty/g2o  
- Click Configure and select Visual Studio 14 2015 x64.  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- Right click on g2o project -> Properties -> General -> Target Extension: .lib, and Configure Type: Static Library (.lib)  
- g2o project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- g2o project -> Properties -> C/C++ Tab -> Preprocessor -> Preprocessor Definitions: add a 'WINDOWS'.  
- Build ALL_BUILD. Finish(g2o.lib).

## Pangolin  
- Open cmake-gui and Make a 'build' directory in ORB-SLAM3forWindows/Thirdparty/Pangolin
- Click Configure and select Visual Studio 14 2015 x64.
- cmake error: could not find git for clone of ... : Disable BUILD_EXTERN_GLEW, LIBJPEG, LIBPNG and input value directly (used GLEW only)  
- If window says Configuring Done, it's OK  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- pangolin project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- Build ALL_BUILD. (ignore error "cannot open input file 'pthread.lib') Finish(pangolin.lib).

## ORB-SLAM3 for Windows  
- Open cmake-gui and make a 'build' directory in ORB-SLAM3forWindows  
- Click Configure and select Visual Studio 14 2015 x64.  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- Setting Boost Library (include, dir, ...)
- Right click on ORB-SLAM3 project -> Properties -> General -> Target Extension: .lib, and Configure Type: Static Library (.lib)  
- ORB-SLAM3 project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- ORB-SLAM3 project -> Properties -> C/C++ Tab -> Preprocessor -> Preprocessor Definitions: check 'COMPILEDWITHC11'.  
- Build ORB-SLAM3 (not ALL_BUILD). Finish(ORB_SLAM3.lib)  

# Test Program
We have tested the following projects: **mono_euroc, mono_inertial_euroc, stereo_euroc, stereo_inertial_euroc**

## example: The EuRoC MAV Dataset: monocular-inertial
- Open **mono_inertial_euroc** directory in ORB-SLAM3forWindows.  
- Change build type to Release.  
- Setting Boost Library (include, dir, ...)  
- Right click on mono_inertial_euroc project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- mono_inertial_euroc project -> Properties -> Linker -> Advanced -> Delete import library.  
- Define 'usleep' function in mono_inertial_euroc.cc
- Build mono_inertial_euroc.  Finish(mono_inertial_euroc.exe).
- **Visual Studio 0xC00000FD: Stack overflow error**: Right click on the project -> Properties -> Linker -> System -> Stack Reserve Size: 8388608(8MB) or more (the default stack size is 1MB = 1048576)
- You will find the test program in ORB-SLAM3forWindows\Examples\Monocular-Inertial\Release.  
- Download the EuRoC MAV Dataset: https://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets
- Convert ORBvoc.txt.tar.gz -> ORBvoc.txt
- Execute the following script:  
`mono_inertial_euroc.exe (path_to_vocabulary) (path_to_settings) (path_to_image_folder_1) (path_to_times_file_1) (path_to_image_folder_2) (path_to_times_file_2) ... (path_to_image_folder_N) (path_to_times_file_N)`
- The result of Machine Hall 01 Dataset (monocular-inertial):  
<img width="980" alt="example_mono_inertial_euroc" src="https://user-images.githubusercontent.com/68829425/88619172-de098a00-d0d5-11ea-8167-2329bd44611a.png">




**Set .lib** 
Configurartion Properties - General - Configurartion type **.lib**
Configurartion Properties - General - Target Extension  **.lib**

**Add lib**
Linker - input - Additional dependencies  - eg,. **E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\lib\Release\pangolin.lib** 
The following should be added (directories may be different):
E:\queenie\ORB-SLAM3forWindows\Thirdparty\g2o\build\Release\g2o.lib 

**Add include**
C/C++ - Additional Include Directories - **E:\queenie\opencv\build\include** 
The following should be added (directories may be different):
E:\queenie\Thirdparty\boost_1_67_0\
E:\queenie\opencv\build\include

**Set MT**
C/C++ - Code generation - Runtime library - **Multi-threaded (/MT)**

**include path list**
E:\queenie\ORB-SLAM3forWindows\Thirdparty\eigen
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\include
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\src\include
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\external\glew\include
E\\\\\\\\\\\\\\\\\
:\queenie\opencv\build\install\include
/////////OR/////////
E:\queenie\opencv\build\include
\\\\\\\\\\\\\\\\\
E:\queenie\ORB-SLAM3forWindows\Thirdparty\boost\boost_1_83_0

**libary path list**
E:\queenie\opencv\build\lib\Release\opencv_world3416.lib
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\external\glew\lib\glew.lib
Release\ORB_SLAM3.lib
\\\\\\\\\\\\\\\\\\\\\\\\\\
E:\queenie\orbslam3-windows\Thirdparty\Pangolin\lib\Release\pangolin.lib
////////////////OR///////////
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\lib\Release\pangolin.lib
\\\\\\\\\\\\\\\\\\\\\\\\\\
glu32.lib
opengl32.lib
E:\queenie\OpenNI2\Lib\OpenNI2.lib
E:\queenie\New folder\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\external\libpng\src\__libpng\projects\visualc71\Win32_LIB_Release\libpng.lib
/////////////////////////
E:\queenie\New folder\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\external\libpng\src\__libpng\projects\visualc71\Win32_LIB_Release\ZLib\zlib.lib
////////////////OR///////////
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\external\zlib\lib\zlibstatic.lib
/////////////////////////
E:\queenie\ORB-SLAM3forWindows\Thirdparty\Pangolin\build\external\libjpeg\src\__libjpeg-build\Release\jpeg.lib
E:\queenie\ORB-SLAM3forWindows\Thirdparty\DBoW2\lib\Release\DBoW2.lib
E:\queenie\ORB-SLAM3forWindows\Thirdparty\g2o\build\Release\g2o.lib
kernel32.lib
user32.lib
gdi32.lib
winspool.lib
shell32.lib
ole32.lib
oleaut32.lib
uuid.lib
comdlg32.lib
advapi32.lib
E:\queenie\boost_1_83_0\lib32-msvc-14.1\libboost_serialization-vc141-mt-s-x32-1_83.lib

# Error
VS2017 MSVCRTD.lib(_chandler4gs_.obj) : error LNK2019: unresolved external symbol __except_handler4_common referenced in function __except_handler4
>>>>put pangolin.lib under openngl32.lib

# Error
Cannot open include file: 'unistd.h': No such file or directory	
adding #include <unistd.h> , you can put it in System.h instead. All other files include System.h in a nested manner.

如果编译的是来自于Linux平台的源文件，该源文件可能会包含头文件 uninstd.h，这样会产生报错信息：
"fatal error C1083: Cannot open include file: 'unistd.h': No such file or directory"

>>create uninstd.h  with the following content:
#ifndef _UNISTD_H
#define _UNISTD_H 
#include <io.h> 
#include <process.h> 
#endif
>>put the uninstd.h in C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.16.27023\include << this directory can be checked out in right click VS project - properties - vc/c++ directory

# Error
Error	LNK1104	cannot open file 'libboost_serialization-**vc141**-mt-s-**x32**-**1_83**.lib'
dowloaded boost-binaries/1.83.0/boost_**1_83**_0-msvc-**14.1**-**32.exe** and execute again
https://sourceforge.net/projects/boost/

Git Bash
./mono_euroc ../../../Vocabulary/ORBvoc.txt ../../../Examples/Monocular/EuRoC.yaml ../../../Examples/Monocular/Release ../../../Examples/Monocular/EuRoC_TimeStamps/MH01.txt dataset-MH01_mono
Command Prompt
mono_euroc.exe ..\..\..\Vocabulary\ORBvoc.txt ..\EuRoC.yaml ..\Release ..\EuRoC_TimeStamps\MH01.txt MH01


# Error 
command no responds after enterring "mono_euroc.exe ..\..\..\Vocabulary\ORBvoc.txt ..\EuRoC.yaml ..\Release ..\EuRoC_TimeStamps\MH01.txt MH01" 
>>> check the correct path of the data!!!

# Error
cannot find opencv_world3416.dll 
>>>>put the dll file into the output path of the project (output path of the mono_euroc.exe)
