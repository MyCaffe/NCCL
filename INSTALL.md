<H2>Installation Instructions</H2>
To build and use <b>NCCL 1.3.4</b> you will need to do the following steps.  As a side note, we are using (and recommend) CUDA 11.0.2 and Visual Studio 2017 on Windows 10 Pro for all of our testing.
</br>
<H3>I. CUDA - Install NVIDIA CUDA and cuDNN Libraries</H3>
Install CUDA 11.0.2 as shown below.
<H4>A. CUDA 11.0.2 - Install NVIDIA CUDA and cuDNN Libraries</H4>
1.) Install the NVIDIA CUDA 11.0.2 Toolkit for Windows 10 from https://developer.nvidia.com/cuda-downloads. 
</br>
<H2>Building NCCL 1.3.4</H2>

** IMPORTANT **
All NCCL builds are 64-bit builds and are only usable by 64-bit applications.

The NCCL solution is configured to build several different versions of NCCL each for a specific version of CUDA. Currently the 'windows/nccl.sln' solution
targets the following NCCL builds:

* nccl.10.0.vcxproj - targets CUDA 10.0 (requires CUDA 10.0 to be installed)
* nccl.10.1.vcxproj - targets CUDA 10.1 (requires CUDA 10.1 to be installed)
* nccl.10.2.vcxproj - targets CUDA 10.2 (requires CUDA 10.2 to be installed)
* nccl.11.0.vcxproj - targets CUDA 11.0 (requires CUDA 11.0 to be installed)

If you only want to target a single version of CUDA (such as CUDA 11), just build the corresponding *.vcxproj noted above.

The resulting DLLs from the build are placed into either the NCCL\windows\x64\Debug or NCCL\windows\x64\Release directory depending
on your build type.  Each resulting DLL file name is appended with the CUDA version that it targets.  So for example
the CUDA 11 version is named 'nccl64_134.11.0.dll' for the release version.

The resulting EXE's for testing are placed into either the NCCL\windows\x64\Debug or NCCL\windows\x64\Release directory
depending on your build type. The following test executables are built:

* all_reduce_scan.exe
* all reduce_test.exe
* broadcast_scan.exe
* broadcast_test.exe
* reduce_scan.exe
* reduce_scatter_scan.exe
* reduce_scatter_test.exe
* reduce_test.exe

Note, the build also copies the required 'cudart64_xxx.dll' into the same directory where the 'xxx' corresponds to the
version of CUDA targeted.

So for example, when targeting CUDA 11, the 'cudart64_110.dll' is copied into the directory.
