# Gromacs Windows Release

Before using the Windows version of Gromacs, it is highly recommended that you install the corresponding CUDA version on your Windows system. The version of `cudatoolkit` should be at least 11.0, otherwise it may cause errors when running **Gromacs 2023.1**. Additionally, during the compilation of Gromacs, it is recommended to use the **MKL** library instead of the **FFTW** library. Therefore, it is best to install the **Intel oneAPI toolkit suite** on your Windows 10/11 system to avoid missing files such as `mkl_core.dll` when running Gromacs.

You can download the Intel oneAPI Base Toolkit using the following link: https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html

![Intel oneAPI Base Toolkit](https://github.com/CondaPereira/Gromacs_windows_Release/blob/main/image/oneapi.png)

If you want to compile Gromacs on your own machine with a Windows system platform, you can read this link's content: https://gitlab.com/gromacs/gromacs/-/issues/4582

I have discovered that when installing the newer versions of Gromacs 2023.1 or Gromacs 2022.x on Windows 10/11, you may encounter a common error during the compilation process in Windows. The error message is `nvcc: unknown std:c++17`. After extensive troubleshooting, I traced this error back to the `gmxManageNvccConfig.cmake` file. I made a modification to a section of the code, as demonstrated in the following image:

![Modified Code](https://github.com/CondaPereira/Gromacs_windows_Release/blob/main/image/modified_code.png)

After making this modification, I was able to successfully compile Gromacs for Windows using CMake (MSVC).

The root cause of this issue lies in the different syntaxes used by NVCC (NVIDIA CUDA Compiler) for the C++17 language standard on Linux and Windows platforms. On one platform, it is `-std:c++17`, while on the other, it is `-std=c++17`.

I highly recommend compiling the Windows version of Gromacs using the following command for version 2021.x. For other versions of Gromacs on Windows, such as 2022.x or 2023.x, it may be necessary to modify the command to ensure successful compilation:

```bash
cmake -GNinja -S. -B./build -DGMX_GPU=CUDA -DGMX_FFT_LIBRARY=mkl \
-DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=off \
-DMKL_INCLUDE_DIR="C:/Program Files (x86)/Intel/oneAPI/mkl/latest/include" \
-DMKL_LIBRARIES="C:/Program Files (x86)/Intel/oneAPI/mkl/latest/lib/intel64/mkl_intel_lp64.lib;C:/Program Files (x86)/Intel/oneAPI/mkl/latest/lib/intel64/mkl_sequential.lib;C:/Program Files (x86)/Intel/oneAPI/mkl/latest/lib/intel64/mkl_core.lib" \
-DCMAKE_INSTALL_PREFIX=C:/gromacs2021.6
```
