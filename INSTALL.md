<H2>Installation Instructions</H2>
To build and use <b>NCCL 1.3.4</b> you will need to do the following steps.  As a side note, we are using (and recommend) CUDA 11.8 and Visual Studio 2022 on Windows 10 Pro for all of our testing.
</br>
<H4>A. Install NVIDIA CUDA Libraries</H4>
1.) Install the NVIDIA CUDA 11.8 Toolkit for Windows 10 from https://developer.nvidia.com/cuda-downloads. 
</br>
<H4>B. Building NCCL 1.3.4</H4>

** IMPORTANT **
All NCCL builds are 64-bit builds and are only usable by 64-bit applications.

The NCCL solution is configured to build several different versions of NCCL each for a specific version of CUDA. Currently the 'windows/nccl.sln' solution
targets the following NCCL builds:

* nccl.11.7.vcxproj - targets CUDA 11.7 (requires CUDA 11.7 to be installed)
* nccl.11.8.vcxproj - targets CUDA 11.8 (requires CUDA 11.8 to be installed)

If you only want to target a single version of CUDA (such as CUDA 11.8), just build the corresponding *.vcxproj noted above.

The resulting DLLs from the build are placed into either the NCCL\windows\x64\Debug or NCCL\windows\x64\Release directory depending
on your build type.  Each resulting DLL file name is appended with the CUDA version that it targets.  So for example
the CUDA 11.8 version is named 'nccl64_134.11.8.dll' for the release version.

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

<H4>Usage</H4>

The 'nccl.h' file located at 'https://github.com/MyCaffe/NCCL/blob/master/src/nccl.h' defines the
main entrypoints into the 'nccl_134_xxx.dll'' several of which are described as follows:

ncclCommInitRank - Creates a new communicator (multi process version).
ncclCommInitAll - Creates a clique of communicators.
ncclCommDestroy - Frees resources associated with communicator object.
ncclAllReduce - Reduces data arrays of length count in sendbuff using op operation, and leaves identical copies of result on each GPUs recvbuff.
ncclBcast - Copies count values from root to all other devices.
ncclGetErrorString - Returns nice error message.

For more function and parameter descriptions and format, callable by the C language, please see 'nccl.h'.

Use the LoadLibrary and GetProcAddress Win32 functions to access each of the 'nccl' functions.  For an example on how to do this, please
see the Initialize method at line 57 of https://github.com/MyCaffe/MyCaffe/blob/master/CudaDnnDLL/Cuda%20Files/nccl.cu.

For more information on programming DLL's in Windows, see https://docs.microsoft.com/en-us/windows/win32/dlls/run-time-dynamic-linking.



