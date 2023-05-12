# Gromacs_windows_Release
Before using the Windows version of Gromacs, it is recommended that you install the corresponding CUDA version on your Windows system. The version of cudatoolkit should be at least 11.0, otherwise it may cause errors when running *Gromacs 2023.1*. Additionally, during the compilation of Gromacs, it is recommended to use the **MKL** library instead of **FFTW** library. Therefore, it is best to install the **Intel oneAPI toolkit suite** on your Windows 10/11 system to avoid missing files such as mkl_core.dll when running Gromacs.

Intel oneAPI base toolkit download link as follows : https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html

