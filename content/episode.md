# Software installation on HPC systems

:::{questions}
- **Should the APP need to be installed on HPC ?**
- **Should I install the APP by myself ?**
:::

A not very accurate metaphor: using HPC looks like renting a room with a shared kitchen, and the landlord has very strict rules.

:::{caution}
as a normal user on HPC system

- no root access
  - no package manager like: apt,yum,dfn …
  - only user's home and project directory 
:::

## Always Start from Reading the Document.

::::{tab-set}

:::{tab-item} LUMI

| LUMI                     |                                               |
| ---                      | ---                                           |
| Location Country         | Finland                                       |
| CPU Architecture         | AMD EPYC                                      |
| GPU Type                 | AMD Instinct MI250X                           |
| User Document/Guide Link | <https://docs.lumi-supercomputer.eu/>         |
| Support Contact          | <https://docs.lumi-supercomputer.eu/support/> |

:::

:::{tab-item} Leonardo

| LEONARDO                 |                                                |
| ---                      | ---                                            |
| Location Country         | Italy                                          |
| CPU Architecture         | Intel Xeon ICE LAKE                            |
| GPU Type                 | NVIDIA A100 SXM4 64GB                          |
| User Document/Guide Link | <https://docs.hpc.cineca.it/hpc/leonardo.html> |
| Support Contact          | superc [AT] cineca.it                          |

:::

:::{tab-item} Vega

| Vega |  |
|---|---|
| Location Country | Slovenia |
| CPU Architecture | AMD EPYC |
| GPU Type | NVIDIA A100 |
| User Document/Guide Link | <https://doc.vega.izum.si/> |
| Support Contact | support [at] sling.si |

:::

:::{tab-item} Karolina

|  Karolina |  |
|---|---|
| Location Country | Czechia |
| CPU Architecture | AMD EPYC |
| GPU Type | NVIDIA A100 |
| User Document/Guide Link | <https://docs.it4i.cz/en/docs/clusters/karolina/introduction/> |
| Support Contact | support [at] it4i.cz |

:::

:::{tab-item} MeluXina

|  MeluXina |  |
|---|---|
| Location Country | Luxembourg |
| CPU Architecture | AMD EPYC |
| GPU Type | NVIDIA A100 |
| User Document/Guide Link | <https://docs.meluxina.eu/> |
| Support Contact |  servicedesk [at] lxp.lu |

:::

:::{tab-item} Deucalion

| Deucalion |  |
|---|---|
| Location Country | Portugal |
| CPU Architecture | ARM A64FX, AMD EPYC |
| GPU Type | NVIDIA A100 |
| User Document/Guide Link | <https://docs.macc.fccn.pt/> |
| Support Contact | deucalion [at] support.macc.fccn.pt |

:::

:::{tab-item} Discoverer

| Discoverer |  |
|---|---|
| Location Country | Bulgaria |
| CPU Architecture | AMD EPYC |
| GPU Type | NVIDIA A100 |
| User Document/Guide Link | <https://docs.discoverer.bg/> |
| Support Contact | helpdesk [at] discoverer.bg |

:::

:::{tab-item} MareNostrum 5

|  MareNostrum 5 |  |
|---|---|
| Location Country | Spain |
| CPU Architecture | Intel Xeon Sapphire Rapids |
| GPU Type | NVIDIA Hopper |
| User Document/Guide Link | <https://www.bsc.es/supportkc/docs/MareNostrum5/intro/> |
| Support Contact | eurohpc_support [at] bsc.es |

:::

::::

## Check What is Already Installed

:::{objectives}

- learn to how to use the `module` tool
- understand what does `module` tool do for you

:::

If you would like to cook in the shared kitchen, it is a good idea to start with checking what kind of cooking wares are provided.

In HPC (High-Performance Computing) systems, the most common tool used to manage installed libraries and applications is 
**Environment module systems**:
using command with `module` or `ml`.

* List all or matching available modules

  ```
  module avail
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster
  ```
    -------------------------------- /leonardo/prod/opt/modulefiles/profiles --------------------------------
  profile/archive            profile/bioinf     profile/deeplrn      profile/global  profile/quantum
  profile/astro              profile/candidate  profile/eng          profile/lifesc  profile/spoke7
  profile/base(default) <L>  profile/chem-phys  profile/geo-inquire  profile/meteo   profile/statistics

  ------------------------------ /leonardo/prod/opt/modulefiles/base/archive ------------------------------
  hysea/3.9.0

  ----------------------------- /leonardo/prod/opt/modulefiles/base/libraries -----------------------------
  adios/1.13.1--hpcx-mpi--2.19--nvhpc--24.5
  adios/1.13.1--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  adios/1.13.1--openmpi--4.1.6--gcc--12.2.0(default)
  blitz/1.0.2--gcc--12.2.0-spack0.22(default)
  blitz/1.0.2--oneapi--2024.1.0
  boost/1.85.0--gcc--12.2.0
  boost/1.85.0--hpcx-mpi--2.19--nvhpc--24.5
  boost/1.85.0--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0-atomic
  boost/1.85.0--oneapi--2024.1.0
  boost/1.85.0--openmpi--4.1.6--gcc--12.2.0(default)
  cgal/5.6--gcc--12.2.0
  cgal/5.6--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  cgal/5.6--oneapi--2024.1.0
  cgal/5.6--openmpi--4.1.6--gcc--12.2.0(default)
  cudnn/8.9.7.29-12--gcc--12.2.0-cuda-12.2(default)
  cutensor/1.5.0.3--gcc--12.2.0(default)
  elpa/2024.03.001--openmpi--4.1.6--gcc--12.2.0-cuda-12.2(default)
  fftw/3.3.10--gcc--12.2.0-spack0.22
  fftw/3.3.10--hpcx-mpi--2.19--nvhpc--24.5
  fftw/3.3.10--hpcx-mpi--2.25.1--nvhpc--25.11
  fftw/3.3.10--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  gdal/3.8.5--gcc--12.2.0(default)
  gsl/2.7.1--gcc--12.2.0-spack0.22(default)
  gsl/2.7.1--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  gsl/2.7.1--nvhpc--24.5
  hdf5/1.14.3--gcc--12.2.0-spack0.22
  hdf5/1.14.3--hpcx-mpi--2.19--nvhpc--24.5
  hdf5/1.14.3--hpcx-mpi--2.25.1--nvhpc--25.11
  hdf5/1.14.3--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  hdf5/1.14.3--oneapi--2024.1.0
  hdf5/1.14.3--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  hpcx-mpi/2.19
  hpcx-mpi/2.25.1
  intel-oneapi-ipp/2021.11.0(default)
  intel-oneapi-mkl/2024.0.0
  intel-oneapi-mkl/2024.0.0--intel-oneapi-mpi--2021.12.1(default)
  intel-oneapi-mpi/2021.12.1(default)
  intel-oneapi-tbb/2021.12.0(default)
  libmatheval/1.1.11--gcc--12.2.0-spack0.22(default)
  libmatheval/1.1.11--oneapi--2024.1.0
  libszip/2.1.1--gcc--12.2.0-spack0.22(default)
  libszip/2.1.1--oneapi--2024.1.0
  magma/2.8.0--gcc--12.2.0-cuda-12.2(default)
  metis/5.1.0--gcc--12.2.0-spack0.22(default)
  metis/5.1.0--nvhpc--24.5
  metis/5.1.0--oneapi--2024.1.0
  nccl/2.22.3-1--gcc--12.2.0-cuda-12.2-spack0.22(default)
  netcdf-c/4.9.2--gcc--12.2.0-spack0.22
  netcdf-c/4.9.2--hpcx-mpi--2.19--nvhpc--24.5
  netcdf-c/4.9.2--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  netcdf-c/4.9.2--oneapi--2024.1.0
  netcdf-c/4.9.2--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  netcdf-fortran/4.6.1--gcc--12.2.0-spack0.22
  netcdf-fortran/4.6.1--hpcx-mpi--2.19--nvhpc--24.5
  netcdf-fortran/4.6.1--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  netcdf-fortran/4.6.1--oneapi--2024.1.0
  netcdf-fortran/4.6.1--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  netlib-scalapack/2.2.0--hpcx-mpi--2.19--nvhpc--24.5
  netlib-scalapack/2.2.0--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  openblas/0.3.26--gcc--12.2.0(default)
  openblas/0.3.26--nvhpc--24.5
  openblas/0.3.26--nvhpc--25.11
  openmpi/4.1.6--gcc--12.2.0-cuda-12.2(default)
  openmpi/5.0.9--gcc--12.2.0-cuda-12.2
  pandacc/2026.01--python--3.11.7
  parallel-netcdf/1.12.3--hpcx-mpi--2.19--nvhpc--24.5
  parallel-netcdf/1.12.3--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  parallel-netcdf/1.12.3--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  parmetis/4.0.3--hpcx-mpi--2.19--nvhpc--24.5
  parmetis/4.0.3--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  parmetis/4.0.3--openmpi--4.1.6--gcc--12.2.0-spack0.22(default)
  petsc/3.22.0--hpcx-mpi--2.19--nvhpc--24.5-mumps-cuda-12.2
  petsc/3.22.0--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0-complex-mumps
  petsc/3.22.0--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0-mumps
  petsc/3.22.0--openmpi--4.1.6--gcc--12.2.0-mumps-cuda-12.2(default)
  proj/9.2.1--gcc--12.2.0-spack0.22(default)
  proj/9.2.1--oneapi--2024.1.0
  py-mpi4py/3.1.5--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  py-mpi4py/3.1.5--openmpi--4.1.6--gcc--12.2.0(default)
  rapids/2023.12(default)
  slate/2023.11.05--openmpi--4.1.6--gcc--12.2.0-cuda-12.2(default)
  slepc/3.22.0--hpcx-mpi--2.19--nvhpc--24.5-cuda-12.2
  slepc/3.22.0--openmpi--4.1.6--gcc--12.2.0-cuda-12.2(default)

  ------------------------------- /leonardo/prod/opt/modulefiles/base/tools -------------------------------
  binutils/2.42
  cdo/2.4.0--gcc--12.2.0(default)
  cintools/1.0 <L>
  cmake/3.27.9(default)
  cmake/4.1.2
  cube/4.8
  curl/8.7.1(default)
  darshan-runtime/3.4.5--openmpi--4.1.6--gcc--12.2.0
  darshan-util/3.4.5--gcc--12.2.0
  dos2unix/7.4.4--gcc--12.2.0
  eccodes/2.33.0--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  eccodes/2.34.0--gcc--12.2.0
  emacs/29.3(default)
  esmf/8.6.0--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  esmf/8.6.0--openmpi--4.1.6--gcc--12.2.0(default)
  firefox/134.0.1
  gdb/14.1--gcc--12.2.0
  ghostscript/10.03.1
  git-lfs/3.1.2
  git/2.45.1(default)
  gmt/6.4.0--gcc--12.2.0(default)
  gnuplot/5.4.3
  grads/2.2.3--openmpi--4.1.6--gcc--12.2.0
  intel-oneapi-advisor/2024.1.0
  intel-oneapi-inspector/2024.1.0(default)
  intel-oneapi-itac/2022.1.0(default)
  intel-oneapi-vtune/2024.1.0(default)
  jube/2.6.1(default)
  linaro/25.0.4
  maven/3.8.4(default)
  ncftp/3.2.6(default)
  nco/5.1.9--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  nco/5.1.9--openmpi--4.1.6--gcc--12.2.0(default)
  ninja/1.11.1
  nvtop/3.1.0
  openjdk/11.0.20.1_1(default)
  osu-micro-benchmarks/7.4--hpcx-mpi--2.19--nvhpc--24.5-cuda-12.2
  osu-micro-benchmarks/7.4--intel-oneapi-mpi--2021.12.1--oneapi--2024.1.0
  osu-micro-benchmarks/7.4--openmpi--4.1.6--gcc--12.2.0-cuda-12.2(default)
  paraview/5.10.1-osmesa
  rcm/v1.2-0.21
  scalasca/2.6.1--hpcx-mpi--2.19--nvhpc--24.5(default)
  scorep/8.4--hpcx-mpi--2.19--nvhpc--24.5-cuda-12.2(default)
  snakemake/8.5.2(default)
  spack/0.22-06(default)
  superc/2.0
  totalview/2025.4
  valgrind/3.20.0--openmpi--4.1.6--gcc--12.2.0

  ----------------------------- /leonardo/prod/opt/modulefiles/base/compilers -----------------------------
  cuda/12.2(default)  intel-oneapi-compilers-classic/2021.10.0(default)  nvhpc/25.11
  cuda/12.3           intel-oneapi-compilers/2024.1.0(default)           perl/5.38.0(default)
  cuda/12.6           llvm/14.0.6--gcc--12.2.0-cuda-12.2(default)        python/3.11.7(default)
  gcc/12.2.0          nvhpc/24.5(default)

  Key:
  (symbolic-version)  <module-tag>  <L>=loaded
  ```
  :::
     or e.g you want to list all modules which match with "intel"
  ```
  module avail intel
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster
  ```
  ----------------------------- /leonardo/prod/opt/modulefiles/base/libraries -----------------------------
  intel-oneapi-ipp/2021.11.0                              intel-oneapi-mpi/2021.12.1
  intel-oneapi-mkl/2024.0.0                               intel-oneapi-tbb/2021.12.0
  intel-oneapi-mkl/2024.0.0--intel-oneapi-mpi--2021.12.1

  ------------------------------- /leonardo/prod/opt/modulefiles/base/tools -------------------------------
  intel-oneapi-advisor/2024.1.0    intel-oneapi-itac/2022.1.0
  intel-oneapi-inspector/2024.1.0  intel-oneapi-vtune/2024.1.0

  ----------------------------- /leonardo/prod/opt/modulefiles/base/compilers -----------------------------
  intel-oneapi-compilers-classic/2021.10.0  intel-oneapi-compilers/2024.1.0

  Key:
  modulepath  default-version
  ```
  :::

* Load modules

  e.g load the gcc with version 12.2.0
  ```
  module load gcc/12.2.0
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  Loading gcc/12.2.0
    Loading requirement: zlib-ng/2.1.6-jkgunjc zstd/1.5.6-uq5yyux binutils/2.42
  ```
  :::

* List loaded modules

  ```
  module list
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  Currently Loaded Modulefiles:
   1) profile/base   3) zlib-ng/2.1.6-jkgunjc   5) binutils/2.42
   2) cintools/1.0   4) zstd/1.5.6-uq5yyux      6) gcc/12.2.0

  Key:
  auto-loaded  default-version
  ```
  :::

* Remove/unload the modules

  e.g remove the module gcc with version 12.2.0
  ```
  module remove gcc/12.2.0
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  Unloading gcc/12.2.0
    Unloading useless requirement: binutils/2.42 zstd/1.5.6-uq5yyux zlib-ng/2.1.6-jkgunjc
  ```
  ```
  $< module list
  Currently Loaded Modulefiles:
   1) profile/base   2) cintools/1.0

  Key:
  default-version
  ```
  :::

  - remove all modules
  ```
  module purge
  ```

* show what is in the module

  ```
  module show gcc/12.2.0
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  -------------------------------------------------------------------
  /leonardo/prod/opt/modulefiles/base/compilers/gcc/12.2.0:

  module-whatis   {The GNU Compiler Collection includes front ends for C, C++, Objective-C, Fortran, Ada, and Go, as well as libraries for these languages.}
  module          load binutils/2.42
  conflict        gcc
  prepend-path    GCC_LIB /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/lib
  prepend-path    LIBRARY_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/lib
  prepend-path    LD_LIBRARY_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/lib
  prepend-path    GCC_LIB /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/lib64
  prepend-path    LIBRARY_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/lib64
  prepend-path    LD_LIBRARY_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/lib64
  prepend-path    GCC_INC /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/include
  prepend-path    GCC_INCLUDE /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/include
  prepend-path    C_INCLUDE_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/include
  prepend-path    CPLUS_INCLUDE_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/include
  prepend-path    CPATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/include
  prepend-path    PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/bin
  prepend-path    MANPATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/share/man
  prepend-path    CMAKE_PREFIX_PATH /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/.
  setenv          CC /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/bin/gcc
  setenv          CXX /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/bin/g++
  setenv          FC /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/bin/gfortran
  setenv          F77 /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz/bin/gfortran
  setenv          GCC_HOME /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-12.2.0-lkcazt4letxjj4s7nlhzryoyivevsatz
  setenv          CC gcc
  setenv          CXX g++
  setenv          FC gfortran
  setenv          F90 gfortran
  setenv          F77 gfortran
  append-path     MANPATH {}
  -------------------------------------------------------------------

  ```
  :::

:::{admonition} Most important compile env vars in practice
:class: dropdown
| Variable | Purpose | Commonly Used By |
|---|---|---|
| `CC` | Select C compiler | `make`, GNU Autoconf, CMake, Meson, Ninja wrappers |
| `CXX` | Select C++ compiler | Autotools, CMake, Meson |
| `FC` | Select modern Fortran compiler | HPC builds, CMake, Autotools |
| `F77` | Select Fortran 77 compiler | Older scientific software |
| `F90` | Select Fortran 90 compiler | Older Fortran projects |
| `CPP` | Select C preprocessor | Configure scripts, Makefiles |
| `AR` | Static archive tool | Link/build systems |
| `LD` | Linker executable | Toolchains, advanced builds |
| `CPATH` | Generic include search path | GCC-family compilers |
| `C_INCLUDE_PATH` | C-only include path | GCC C frontend |
| `CPLUS_INCLUDE_PATH` | C++-only include path | GCC C++ frontend |
| `LIBRARY_PATH` | Library search path during linking | GCC linker driver |
| `LD_LIBRARY_PATH` | Runtime shared library search path | Linux dynamic loader (`ld.so`) |
| `LD_PRELOAD` | Force-load shared libraries | Linux runtime loader |
| `LD_RUN_PATH` | Embed runtime library path | Linker/runtime |
| `PATH` | Executable search path | Shells, all programs |
| `PKG_CONFIG_PATH` | Search path for `.pc` files | `pkg-config` |
| `PKG_CONFIG_LIBDIR` | Override pkg-config system dirs | `pkg-config` |
| `CMAKE_PREFIX_PATH` | Prefixes for package discovery | CMake |
| `CMAKE_MODULE_PATH` | Additional CMake modules | CMake |
| `MPICC` | MPI C compiler wrapper | MPI/HPC builds |
| `MPICXX` | MPI C++ compiler wrapper | MPI/HPC builds |
| `MPIFC` | MPI Fortran compiler wrapper | MPI/HPC builds |
| `MPIF77` | MPI F77 wrapper | Older MPI software |
| `CUDA_HOME` | CUDA toolkit root | CUDA builds, ML frameworks |

| Variable | Purpose | Commonly Used By |
|---|---|---|
| `CFLAGS` | C compiler flags | GCC/Clang via Makefiles, Autotools |
| `CXXFLAGS` | C++ compiler flags | C++ builds |
| `FCFLAGS` | Modern Fortran compiler flags | Fortran projects |
| `FFLAGS` | Legacy Fortran flags | Older Fortran builds |
| `CPPFLAGS` | Preprocessor flags | GCC, Clang, configure scripts |
| `LDFLAGS` | Linker flags | Link stages in most build systems |
| `LIBS` | Libraries to link | Configure scripts, Makefiles |
:::

## A Quick Revisit of How to Compile Source Code into Library and Executable 


Here we use a simple example as demo:

- mylib: click to download {download}`mylib.tar`

  mylib is library contains only 1 function of naive matrix multiplication {math}`C_{ij} = \sum_k A_{ik} \times B_{kj} + C_{ij}`

  ```
  mylib
  ├── include
  │   └── mymath.h
  └── src
      └── mymath.c
  ```

- myapp: click to download {download}`myapp.tar`
  
  myapp benchmark the naive matrix multiplication from mylib and also `gemm` from cblas library.

  ```
  myapp
  └── src
      └── main.c
  ```
### manually compile the source code

:::{objectives}

- understand

  - compiler flag `-I` and env var `C_INCLUDE_PATH` or `CPATH`
  - compiler flag `-L` and env var `LIBRARY_PATH`
  - environment variable `LD_LIBRARY_PATH`
  - compiler flag `-O3`
  - use compiler preprocessor flag `-D`

- use `ldd` check linked dynamic libraries

:::

- create shared library

  ```
  gcc --shared mymath.c -o libmylib.so
  ```

- compile main.c to "obj"

  ```
  gcc -c myapp.c
  ```
  you may get error message:
  :::{admonition} output

  ```
  main.c:5:10: fatal error: mymath.h: No such file or directory
   #include "mymath.h"
            ^~~~~~~~~~
  compilation terminated.
  ```

  you can choose from:

  - use env variable `C_INCLUDE_PATH` or `CPATH`

    ```
    C_INCLUDE_PATH=../../mylib/include gcc -c main.c
    ```

    ```
    CPATH=../../mylib/include gcc -c main.c
    ```
  - use compiler flag `-I`
  
    ```
    gcc -I ../../mylib/include -c main.c
    ```
  :::

- create the myapp.exe with linking main.o and libmylib.so

  ```
     gcc -o myapp.exe main.o -lmylib
  ```
  you may get error message:
  :::{admonition} output

  ```
  /usr/lib64/gcc/x86_64-suse-linux/7/../../../../x86_64-suse-linux/bin/ld: cannot find -lmylib: No such file or directory
  collect2: error: ld returned 1 exit status
  ```

  you can choose from:

  - use env variable `LIBRARY_PATH`

    ```
    LIBRARY_PATH=../../mylib/ gcc -o myapp.exe main.o -lmylib
    ```
  - use compiler flag `-L`
  
    ```
    gcc -o myapp.exe main.o -L ../../mylib/ -lmylib
    ```
  :::

- run the myapp.exe
  
  ```
  ./myapp.exe
  ```
  you may get error message:
  :::{admonition} output

  ```
  ./myapp.exe: error while loading shared libraries: libmylib.so: cannot open shared object file: No such file or directory
  ```
  let's check what libraries myapp.exe linked with

  ```
  ldd ./myapp.exe
  ```
  output:

  ```
	linux-vdso.so.1 (0x00007ffe281bb000)
	libmylib.so => not found
	libc.so.6 => /lib64/libc.so.6 (0x0000146264f43000)
	/lib64/ld-linux-x86-64.so.2 (0x0000146265170000)
  ```

  **libmylib.so => not found**

  use env variable `LD_LIBRARY_PATH`

  ```
  LD_LIBRARY_PATH=../../mylib/ ldd ./myapp.exe
  ```
  output:

  ```
  linux-vdso.so.1 (0x00007fff71de5000)
  libmylib.so => ../../mylib/libmylib.so (0x000015105741f000)
  libc.so.6 => /lib64/libc.so.6 (0x00001510571f4000)
  /lib64/ld-linux-x86-64.so.2 (0x0000151057424000)
  ```

  now run with:

  ```
  LD_LIBRARY_PATH=../../mylib/ ./myapp.exe
  ```

  output:

  ```
  Benchmarking GEMM (Size: 512x512, Trials: 100)
  --------------------------------------------------
  Manual GEMM (Avg): 0.616966 seconds, checksum= 5171200.000000
  ```
  :::

- compile mylib with `-O3`

  ```{code-block} bash
  :lineno-start: 1
  cd mylib/src
  gcc -O3 --shared mymath.c -o ../libmylib.so
  cd -
  cd myapp/src
  gcc -I ../../mylib/include -c main.c
  gcc -o myapp.exe main.o -L ../../mylib/ -lmylib
  LD_LIBRARY_PATH=../../mylib/ ./myapp.exe
  ```
  output:

  ```
  Benchmarking GEMM (Size: 512x512, Trials: 100)
  --------------------------------------------------
  Manual GEMM (Avg): 0.062695 seconds, checksum= 5171200.000000
  ```
  compare to time without `-O3`, myapp.exe almost has 10x speed

- with `-D CBLAS` to call cblas_dgemm
  
  ```{code-block} c
  :lineno-start: 43
  #ifdef CBLAS
      // 1. Warm-up (Ensures CPU is out of power-saving mode)
      cblas_dgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans,
                      N, N, N, 1.0, A, N, B, N, 0.0, C, N);
      for (int i = 0; i < N * N; i++) { C[i] = 0.0; }

      checksum = 0.0;
      // 2. Benchmark BLAS DGEMM
      start = get_time();
      for(int t = 0; t < TAIALS; t++) {
          cblas_dgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans,
                      N, N, N, 1.0, A, N, B, N, 1.0, C, N);
          checksum += C[t];
      }
      end = get_time();
      printf("System BLAS (Avg): %f seconds, checksum= %f\n", (end - start) / TAIALS, checksum);
  #endif
  ```
  compile the main.c same as above, simply add `-D CBLAS`.
  we also need let the compiler find the header file: `cblas.h` and link to the BLAS library.

  ::::{tab-set}

  :::{tab-item} LUMI with libsci
  ```
  ml purge
  ml LUMI/25.03 partition/C PrgEnv-gnu
  cd mylib/src
  cc -O3 --shared mymath.c -o ../libmylib.so
  cd -
  cd myapp/src
  cc -I ../../mylib/include -c -DCBLAS main.c
  cc -o myapp.exe main.o -L ../../mylib/ -lmylib
  LD_LIBRARY_PATH=../../mylib/ ./myapp.exe
  ```
  output:

  ```
  Benchmarking GEMM (Size: 512x512, Trials: 100)
  --------------------------------------------------
  Manual GEMM (Avg): 0.060575 seconds, checksum= 5171200.000000
  System BLAS (Avg): 0.005845 seconds, checksum= 5171200.000000
  ```
  with dgemm from highly optimized BLAS library provided by Cray libsci, we get another 10x speed

  ```{code-block} bash
  :emphasize-lines:4
  LD_LIBRARY_PATH=../../mylib/ ldd myapp.exe
	linux-vdso.so.1 (0x00007ffe7ddf1000)
	libmylib.so => ../../mylib/libmylib.so (0x0000154025ba7000)
	libsci_gnu.so.6 => /opt/cray/pe/lib64/libsci_gnu.so.6 (0x0000154023522000)
	libxpmem.so.0 => /usr/lib64/libxpmem.so.0 (0x000015402351f000)
	libc.so.6 => /lib64/libc.so.6 (0x0000154023308000)
	libgfortran.so.5 => /usr/lib64/libgfortran.so.5 (0x0000154023003000)
	libm.so.6 => /lib64/libm.so.6 (0x0000154022f19000)
	/lib64/ld-linux-x86-64.so.2 (0x0000154025bac000)
	libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x0000154022eec000)
  ```
  :::

  :::{tab-item} Leonardo with mkl
  ```
  ml purge
  ml gcc/12.2.0 intel-oneapi-mkl/2024.0.0
  cd mylib/src
  gcc -O3 --shared mymath.c -o ../libmylib.so
  cd -
  cd myapp/src; sed -i 's/<cblas.h>/<mkl_cblas.h>/' main.c
  gcc -I ../../mylib/include -c -DCBLAS main.c
  gcc -o myapp.exe main.o -L ../../mylib/ -lmylib -Wl,--no-as-needed -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -lpthread -lm -ldl
  LD_LIBRARY_PATH=../../mylib/:$LD_LIBRARY_PATH ./myapp.exe
  ```
  output:

  ```
  Benchmarking GEMM (Size: 512x512, Trials: 100)
  --------------------------------------------------
  Manual GEMM (Avg): 0.033518 seconds, checksum= 5171200.000000
  System BLAS (Avg): 0.003465 seconds, checksum= 5171200.000000
  ```
  with dgemm from highly optimized BLAS library provided by MKL, we get another 10x speed

  ```{code-block} bash
  :emphasize-lines:4
  LD_LIBRARY_PATH=../../mylib/:$LD_LIBRARY_PATH ldd ./myapp.exe
	linux-vdso.so.1 (0x00007ffc23bb9000)
	libmylib.so => ../../mylib/libmylib.so (0x00007f39bfb08000)
	libmkl_intel_lp64.so.2 => /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/intel-oneapi-mkl-2024.0.0-vexzfithc53dsedryb625yywykakdg7m/mkl/2024.0/lib/libmkl_intel_lp64.so.2 (0x00007f39be3d1000)
	libmkl_sequential.so.2 => /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/intel-oneapi-mkl-2024.0.0-vexzfithc53dsedryb625yywykakdg7m/mkl/2024.0/lib/libmkl_sequential.so.2 (0x00007f39bcfc9000)
	libmkl_core.so.2 => /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/intel-oneapi-mkl-2024.0.0-vexzfithc53dsedryb625yywykakdg7m/mkl/2024.0/lib/libmkl_core.so.2 (0x00007f39b8e97000)
	libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f39b8c77000)
	libm.so.6 => /lib64/libm.so.6 (0x00007f39b88f5000)
	libdl.so.2 => /lib64/libdl.so.2 (0x00007f39b86f1000)
	libc.so.6 => /lib64/libc.so.6 (0x00007f39b831a000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f39bf8e0000)
  ```
  :::

  ::::

:::{admonition} Common Compilers
:class: dropdown

| Vendor / Project | C Compiler | C++ Compiler | Fortran Compiler | Notes |
|---|---|---|---|---|
| GNU | `gcc` | `g++` | `gfortran` | Most widely available, open-source, default on many Linux systems, strong community support |
| LLVM / Clang | `clang` | `clang++` | `flang` (new LLVM Flang) | Modern LLVM-based compiler infrastructure, fast compilation, widely used as a backend for many vendor compilers |
| Intel (oneAPI) | `icx` (`icc` legacy) | `icpx` (`icpc` legacy) | `ifx` (`ifort` legacy) | LLVM-based modern compilers optimized for Intel CPUs with strong vectorization and HPC performance |
| NVIDIA HPC SDK (NVHPC) | `nvc` | `nvc++` | `nvfortran` | Optimized for CPU+GPU systems, supports OpenACC, OpenMP offloading, and CUDA-aware HPC workflows |
| Cray / HPE Cray Compiler Environment (CCE) | `craycc` | `crayCC` | `crayftn` | Designed for Cray supercomputers with strong MPI and scalability optimizations |
| AMD Optimizing C/C++ Compiler (AOCC) | `clang` | `clang++` | `flang` | LLVM-based compiler suite optimized for AMD EPYC processors and Zen architecture |
:::

### compile the source code with makefile or cmake

:::{objectives}

- briefly understand 
  - how to use makefile to build your app
  - how to use cmake to build your app

- use module file to manage your lib and apps for different version

:::

#### check out the `make` branch of mylib

  ```
  cd mylib
  git checkout make
  tree
  .
  ├── CMakeLists.txt
  ├── include
  │   └── mymath.h
  ├── makefile
  ├── modulefile
  └── src
      └── mymath.c

  2 directories, 5 files
  ```
:::::{tab-set}

::::{tab-item} makefile
demo on Leonardo Booster

- use gcc to build and install to APP/mylib 

  ```
  make PREFIX=../APP/mylib/1.0.0 install
  make clean
  make PREFIX=../APP/mylib/2.0.0 CFLAGS=-O3 install
  ```
- create modulefiles in APP/modules/mylib

  ```
  sed "s:XXXXXX*:$(dirname $(pwd))/APP/mylib/1.0.0/:" modulefile > ../APP/modules/mylib/1.0.0
  sed "s:XXXXXX*:$(dirname $(pwd))/APP/mylib/2.0.0/:" modulefile > ../APP/modules/mylib/2.0.0
  ```
- use APP/modules as module path 

  ```
  cd ../APP/modules
  module use `pwd`
  module avail mylib
  ```
  :::{admonition} output
  :class: dropdown

  ```
  --------------- /leonardo/home/userexternal/wli00000/webinar/demo/APP/modules ---------------
  mylib/1.0.0  mylib/2.0.0

  Key:
  loaded  modulepath
  ```
  :::

::::

::::{tab-item} cmake
demo on Leonardo Booster

- use gcc to build and install to APP/mylib 

  ```
  cmake -B build01 -DCMAKE_INSTALL_PREFIX=$(dirname $PWD)/APP/mylib/1.0.0
  cd build01
  make install
  cd -
  cmake -B build02 -DCMAKE_C_FLAGS='-O3' -DCMAKE_INSTALL_PREFIX=$(dirname $PWD)/APP/mylib/2.0.0
  cd build02
  make install
  ```
- create modulefiles in APP/modules/mylib

  ```
  sed "s:XXXXXX*:$(dirname $(pwd))/APP/mylib/1.0.0/:" modulefile > ../APP/modules/mylib/1.0.0
  sed "s:XXXXXX*:$(dirname $(pwd))/APP/mylib/2.0.0/:" modulefile > ../APP/modules/mylib/2.0.0
  ```

- use APP/modules as module path 

  ```
  cd ../APP/modules
  module use `pwd`
  module avail mylib
  ```
  :::{admonition} output
  :class: dropdown

  ```
  --------------- /leonardo/home/userexternal/wli00000/webinar/demo/APP/modules ---------------
  mylib/1.0.0  mylib/2.0.0

  Key:
  loaded  modulepath
  ```
  :::
::::

:::::

#### check out the `make` branch of myapp

  ```
  cd myapp
  git checkout make
  tree
  .
  ├── CMakeLists.txt
  ├── makefile
  ├── modulefile
  └── src
      └── main.c

  1 directory, 4 files
  ```
:::::{tab-set}

::::{tab-item} makefile
demo on Leonardo Booster

- load mylib/2.0.0
  
  ```
  module load mylib/2.0.0
  ```
- chose to compile with openblas

  ```
  module load openblas/0.3.26--gcc--12.2.0
  make clean
  make PREFIX=../APP/myapp/gcc-12.2.0-openblas-0.3.26 USE_CBLAS=1 BLAS=openblas install
  ```

- chose to compile with mkl

  ```
  module load intel-oneapi-mkl/2024.0.0
  make clean
  make PREFIX=../APP/myapp/gcc-12.2.0-intel-oneapi-mkl-2024.0.0 USE_CBLAS=1 BLAS=mkl install
  ```

- create modulefiles in APP/modules/myapp

  ```
  cp modulefile ../APP/modules/myapp/gcc-12.2.0-openblas-0.3.26 
  cp modulefile ../APP/modules/myapp/gcc-12.2.0-intel-oneapi-mkl-2024.0.0
  # need modify these 2 files
  ```

  ```
  module avail myapp
  ```
  :::{admonition} output
  :class: dropdown

  ```
  --------------- /leonardo/home/userexternal/wli00000/webinar/demo/APP/modules ---------------
  myapp/gcc-12.2.0-intel-oneapi-mkl-2024.0.0  myapp/gcc-12.2.0-openblas-0.3.26

  Key:
  modulepath
  ```
  :::

::::


::::{tab-item} cmake
demo on Leonardo Booster

- load mylib/2.0.0
  
  ```
  module load mylib/2.0.0
  ```
- chose to compile with openblas

  ```
  module load openblas/0.3.26--gcc--12.2.0
  cmake -B build01 -DUSE_CBLAS=on \
  -DCMAKE_INSTALL_PREFIX=$(dirname $PWD)/APP/myapp/gcc-12.2.0-openblas-0.3.26
  cd build01
  make install
  ```

- chose to compile with mkl

  ```
  module load intel-oneapi-mkl/2024.0.0
  cmake -B build02 -DUSE_CBLAS=on \
  -DCMAKE_INSTALL_PREFIX=$(dirname $PWD)/APP/myapp/gcc-12.2.0-intel-oneapi-mkl-2024.0.0
  cd build02
  make install
  ```

- create modulefiles in APP/modules/myapp

  ```
  cp modulefile ../APP/modules/myapp/gcc-12.2.0-openblas-0.3.26 
  cp modulefile ../APP/modules/myapp/gcc-12.2.0-intel-oneapi-mkl-2024.0.0
  # need modify these 2 files
  ```

  ```
  module avail myapp
  ```
  :::{admonition} output
  :class: dropdown

  ```
  --------------- /leonardo/home/userexternal/wli00000/webinar/demo/APP/modules ---------------
  myapp/gcc-12.2.0-intel-oneapi-mkl-2024.0.0  myapp/gcc-12.2.0-openblas-0.3.26

  Key:
  modulepath
  ```
  :::

::::

:::::

## **spack**: a package manager for supercomputers

useful links:
- official webpage: [ https://spack.io/ ](https://spack.io/)

### quick start:

```
git clone --depth=2 https://github.com/spack/spack.git
cd spack/bin
./spack install libelf
```

### demo on Leonardo

```
module avail spack
```
:::{admonition} output
:class: dropdown

```
------------------------------- /leonardo/prod/opt/modulefiles/base/tools -------------------------------
spack/0.22-06

Key:
loaded  modulepath  default-version
```
:::

```
module load spack/0.22-06
```
:::{admonition} output
:class: dropdown

```
Spack activated with install: /leonardo/pub/userexternal/wli00000/spack-0.22.2-06/install , modules: /leonardo/pub/userexternal/wli00000/spack-0.22.2-06/modules and cache: /leonardo/pub/userexternal/wli00000/spack-0.22.2-06/cache
```
:::

- check which env vars set for the spack

  ```
  env | grep -i ^spack
  ```

- check which compilers already installed/setup 

  ```
  spack compilers
  ```
  :::{admonition} output
  :class: dropdown

  ```
  ==> Available compilers
  -- gcc rhel8-x86_64 ---------------------------------------------
  gcc@8.5.0  gcc@12.2.0

  -- intel rhel8-x86_64 -------------------------------------------
  intel@2021.10.0

  -- nvhpc rhel8-x86_64 -------------------------------------------
  nvhpc@25.11  nvhpc@24.5

  -- oneapi rhel8-x86_64 ------------------------------------------
  oneapi@2024.1.0
  ```
  :::

- check which packages are already installed

  ```
  spack find
  ```
  :::{admonition} output
  :class: dropdown

  ```
  -- linux-rhel8-icelake / gcc@8.5.0 ------------------------------
  anaconda3@2023.09-0                       openssh@9.7p1
  autoconf@2.72                             openssl@1.1.1k
  autoconf-archive@2023.02.20               patchelf@0.17.2
  automake@1.16.5                           pcre@8.45
  bdw-gc@8.2.6                              pcre2@10.43
  berkeley-db@18.1.40                       perl@5.38.0
  binutils@2.42                             pigz@2.8
  binutils@2.42                             pkgconf@2.2.0
  bison@3.8.2                               pmix@3.1.5
  bzip2@1.0.8                               popt@1.16
  check@0.15.2                              py-appdirs@1.4.4
  cmake@3.27.9                              py-argparse-dataclass@2.0.0
  cmake@4.1.2                               py-attrs@23.1.0
  conmon@2.1.7                              py-calver@2022.6.26
  cryptsetup@2.3.5                          py-certifi@2023.7.22
  cuda@12.2.0                               py-charset-normalizer@3.3.0
  curl@8.7.1                                py-conda-inject@1.3.1
  diffutils@3.10                            py-configargparse@1.7
  elfutils@0.190                            py-connectionpool@0.0.3
  emacs@29.3                                py-cython@0.29.36
  environment-modules@5.4.0                 py-datrie@0.8.2
  expat@2.6.2                               py-docutils@0.20.1
  findutils@4.9.0                           py-dpath@2.1.6
  gawk@5.3.0                                py-editables@0.3
  gcc@12.2.0                                py-fastjsonschema@2.16.3
  gcc-runtime@8.5.0                         py-flit-core@3.9.0
  gdbm@1.23                                 py-gitdb@4.0.9
  gdrcopy@2.4.1                             py-gitpython@3.1.40
  gettext@0.22.5                            py-hatch-fancy-pypi-readme@23.1.0
  git@2.45.1                                py-hatch-nodejs-version@0.3.1
  glib@2.78.3                               py-hatch-vcs@0.3.0
  glibc@2.28                                py-hatchling@1.21.0
  glpk@5.0                                  py-humanfriendly@10.0
  gmake@4.4.1                               py-idna@3.4
  gmp@6.2.1                                 py-immutables@0.20
  gnutls@3.8.3                              py-jinja2@3.1.2
  go@1.22.2                                 py-jsonschema@4.17.3
  go-bootstrap@1.20.6                       py-jupyter-core@5.3.0
  go-md2man@2.0.3                           py-markupsafe@2.1.3
  gperf@3.1                                 py-nbformat@5.8.0
  guile@2.2.6                               py-packaging@23.1
  gzip@1.13                                 py-pathspec@0.11.1
  hcoll@4.8.3227                            py-pip@23.1.2
  hpcx-mpi@2.19                             py-plac@1.3.5
  hpcx-mpi@2.25.1                           py-platformdirs@3.10.0
  hwloc@2.2.0                               py-pluggy@1.4.0
  hwloc@2.2.0                               py-poetry-core@1.8.1
  intel-oneapi-advisor@2024.1.0             py-psutil@5.9.5
  intel-oneapi-compilers@2023.2.4           py-pulp@2.6.0
  intel-oneapi-compilers@2024.1.0           py-pyrsistent@0.19.3
  intel-oneapi-compilers-classic@2021.10.0  py-pytest-runner@6.0.0
  intel-oneapi-inspector@2024.1.0           py-pyyaml@6.0
  intel-oneapi-ipp@2021.11.0                py-requests@2.31.0
  intel-oneapi-itac@2022.1.0                py-reretry@0.11.8
  intel-oneapi-mkl@2024.0.0                 py-ruamel-yaml@0.17.32
  intel-oneapi-mkl@2024.0.0                 py-ruamel-yaml-clib@0.2.7
  intel-oneapi-mpi@2021.12.1                py-setuptools@69.2.0
  intel-oneapi-tbb@2021.12.0                py-setuptools-scm@8.0.4
  intel-oneapi-vtune@2024.1.0               py-smart-open@5.2.1
  json-c@0.16                               py-smmap@5.0.0
  jube@2.6.1                                py-snakemake-interface-common@1.17.1
  knem@1.1.4.90mlnx1                        py-snakemake-interface-executor-plugins@8.2.0
  krb5@1.20.1                               py-snakemake-interface-report-plugins@1.0.0
  less@643                                  py-snakemake-interface-storage-plugins@3.1.0
  libaio@0.3.113                            py-stopit@1.1.2
  libatomic-ops@7.8.0                       py-tabulate@0.8.9
  libbsd@0.12.1                             py-throttler@1.2.2
  libedit@3.1-20230828                      py-tomli@2.0.1
  libevent@2.1.6                            py-toposort@1.10
  libffi@3.4.6                              py-traitlets@5.9.0
  libfuse@3.16.2                            py-trove-classifiers@2023.8.7
  libgpg-error@1.49                         py-typing-extensions@4.8.0
  libiconv@1.17                             py-urllib3@2.1.0
  libidn2@2.3.7                             py-wheel@0.41.2
  libjpeg-turbo@3.0.0                       py-wrapt@1.15.0
  libmd@1.0.4                               py-yte@1.5.1
  libseccomp@2.5.4                          python@3.11.7
  libsigsegv@2.14                           python-venv@1.0
  libtool@2.4.7                             rdma-core@43.0
  libunistring@1.2                          re2c@2.2
  libxcrypt@4.4.35                          readline@8.2
  libxml2@2.10.3                            rust-bootstrap@1.88.0
  libyaml@0.2.5                             shadow@4.13
  lustre@2.14.0_ddn125                      singularityce@4.1.0
  lvm2@2.03.14                              slurm@22.05.10
  m4@1.4.19                                 snakemake@8.5.2
  maven@3.8.4                               sqlite@3.43.2
  meson@1.3.2                               squashfs@4.6.1
  mpc@1.3.1                                 tar@1.34
  mpfr@4.2.1                                tcl@8.6.12
  nasm@2.15.05                              texinfo@7.0.3
  ncftp@3.2.6                               ucc@1.3.0
  ncurses@6.5                               ucx@1.16.0
  nettle@3.9.1                              util-linux@2.40
  nghttp2@1.57.0                            util-linux-uuid@2.38.1
  ninja@1.11.1                              xz@5.4.6
  nvhpc@24.5                                yasm@1.3.0
  nvhpc@25.11                               zlib-ng@2.1.6
  nvptx-tools@2023-09-13                    zoltan@3.901
  openjdk@11.0.20.1_1                       zstd@1.5.6

  -- linux-rhel8-icelake / gcc@12.2.0 -----------------------------
  adios@1.13.1        geos@3.12.1                   libxfont@1.5.4            py-fypp@3.1
  alsa-lib@1.2.3.2    glibc@2.28                    llvm@14.0.6               py-gast@0.5.4
  antlr@2.7.7         gobject-introspection@1.78.1  lua@5.3.6                 py-meson-python@0.15.0
  arpack-ng@3.9.0     gromacs@2024.2                lz4@1.9.4                 py-mpi4py@3.1.5
  atompaw@4.2.0.3     gromacs@2024.2                lzo@2.10                  py-numpy@1.26.4
  bdftopcf@1.1        gromacs@2024.2                magma@2.8.0               py-pip@23.0
  blaspp@2023.11.05   gsl@2.7.1                     mctc-lib@0.3.1            py-ply@3.11
  blitz@1.0.2         hdf5@1.14.3                   metis@5.1.0               py-pybind11@2.12.0
  boost@1.85.0        hdf5@1.14.3                   mkfontdir@1.0.7           py-pyproject-metadata@0.7.1
  boost@1.85.0        help2man@1.49.3               mkfontscale@1.2.3         py-pythran@0.15.0
  boost@1.85.0        htslib@1.19.1                 multicharge@0.3.0         py-scipy@1.13.0
  c-blosc@1.21.5      hwloc@2.2.0                   mumps@5.6.2               r@4.4.0
  cairo@1.16.0        hypre@2.31.0                  namd@3.0                  rsync@3.2.7
  cdo@2.4.0           icu4c@67.1                    namd@3.0                  samtools@1.19.2
  cfitsio@4.3.0       inputproto@2.3.2              namd@3.0                  slate@2023.11.05
  cgal@5.6            json-c@0.16                   nccl@2.22.3-1             slepc@3.22.0
  cgal@5.6            kbproto@1.0.7                 nco@5.1.9                 snappy@1.1.10
  charmpp@7.0.0       knem@1.1.4.90mlnx2            netcdf-c@4.9.2            superlu-dist@8.2.1
  charmpp@7.0.0       lapackpp@2023.11.05           netcdf-c@4.9.2            swig@4.0.2-fortran
  cp2k@2024.1         libaec@1.0.6                  netcdf-fortran@4.6.1      swig@4.1.1
  cudnn@8.9.7.29-12   libarchive@3.7.1              netcdf-fortran@4.6.1      sz@1.4.12.3
  curl@8.7.1          libcerf@1.3                   netlib-scalapack@2.2.0    ucc@1.6.0
  cutensor@1.5.0.3    libdeflate@1.18               numactl@2.0.14            ucx@1.16.0
  dftd4@3.7.0         libfontenc@1.1.8              openblas@0.3.26           ucx@1.20.0
  eccodes@2.34.0      libgeotiff@1.7.1              openblas@0.3.26           udunits@2.2.28
  eigen@3.4.0         libice@1.1.1                  openjpeg@2.3.1            unzip@6.0
  elfutils@0.190      libint@2.6.0                  openmpi@4.1.6             util-macros@1.19.3
  elpa@2024.03.001    libmatheval@1.1.11            openmpi@5.0.9             valgrind@3.20.0
  esmf@8.6.0          libmicrohttpd@0.9.50          osu-micro-benchmarks@7.4  vasp@6.4.3
  fftw@3.3.10         libpng@1.6.39                 papi@7.1.0                wannier90@3.1.0
  fftw@3.3.10         libpthread-stubs@0.5          parallel-netcdf@1.12.3    which@2.21
  flex@2.6.3          libsm@1.2.4                   parallelio@2.6.2          xcb-proto@1.16.0
  flex@2.6.4          libszip@2.1.1                 parmetis@4.0.3            xextproto@7.3.0
  font-util@1.4.0     libtiff@4.5.1                 perl-data-dumper@2.173    xproto@7.0.31
  fontconfig@2.15.0   libtirpc@1.3.3                petsc@3.22.0              xtrans@1.5.0
  fontsproto@2.1.3    libx11@1.8.7                  pixman@0.42.2             xxhash@0.8.1
  freetype@2.13.2     libxau@1.0.11                 plumed@2.9.2              zfp@0.5.5
  fribidi@1.0.12      libxc@7.0.0                   pmix@5.0.1                zlib@1.3.1
  gcc-runtime@12.2.0  libxc@7.0.0                   proj@9.2.1
  gdal@3.8.5          libxcb@1.16                   py-beniget@0.4.1
  gdb@14.1            libxdmcp@1.1.4                py-cython@3.0.8

  -- linux-rhel8-icelake / intel@2021.10.0 ------------------------
  abinit@10.0.9  charmpp@7.0.0  charmpp@7.0.0  hypre@2.31.0  namd@3.0  openfoam-org@6  openfoam-org@2.1.1

  -- linux-rhel8-icelake / nvhpc@24.5 -----------------------------
  adios@1.13.1      hdf5@1.14.3   netcdf-c@4.9.2            parallel-netcdf@1.12.3  slepc@3.22.0
  boost@1.85.0      hypre@2.31.0  netcdf-fortran@4.6.1      parmetis@4.0.3          slepc@3.22.0
  cubelib@4.8.2     libxc@5.2.3   netlib-scalapack@2.2.0    petsc@3.22.0            superlu-dist@8.2.1
  cubew@4.8.2       libxc@7.0.0   opari2@2.0.8              petsc@3.22.0            yambo@5.3.0
  devicexlib@0.8.6  metis@5.1.0   openblas@0.3.26           quantum-espresso@7.4.1
  fftw@3.3.10       mumps@5.6.2   osu-micro-benchmarks@7.4  scalasca@2.6.1
  gsl@2.7.1         mumps@5.6.2   otf2@3.0.3                scorep@8.4

  -- linux-rhel8-icelake / nvhpc@25.11 ----------------------------
  fftw@3.3.10  hdf5@1.14.3  openblas@0.3.26

  -- linux-rhel8-icelake / oneapi@2024.1.0 ------------------------
  abseil-cpp@20240116.2  hdf5@1.14.3                    namd@3.0                  petsc@3.22.0
  adios@1.13.1           hdf5@1.14.3                    namd@3.0                  petsc@3.22.0
  adios2@2.8.3           hypre@2.31.0                   nco@5.1.9                 plumed@2.9.2
  antlr@2.7.7            intel-oneapi-runtime@2024.1.0  netcdf-c@4.9.2            proj@9.2.1
  blitz@1.0.2            libarchive@3.7.1               netcdf-c@4.9.2            protobuf@3.25.3
  boost@1.85.0           libfabric@1.21.0               netcdf-c@4.9.2            py-fypp@3.1
  boost@1.85.0           libgeotiff@1.7.1               netcdf-fortran@4.6.1      py-mpi4py@3.1.5
  cgal@5.6               libmatheval@1.1.11             netcdf-fortran@4.6.1      py-numpy@1.26.4
  cgal@5.6               libszip@2.1.1                  netcdf-fortran@4.6.1      scotch@7.0.4
  eccodes@2.33.0         libvori@220621                 nwchem@7.2.2              sed@4.9
  esmf@8.6.0             libxc@5.2.3                    openfoam@2512             superlu-dist@8.2.1
  fftw@3.3.10            libxc@7.0.0                    openfoam-org@13           yaml-cpp@0.7.0
  gromacs@2024.2         lzo@2.10                       osu-micro-benchmarks@7.4  zfp@0.5.5
  gromacs@2024.2         metis@5.1.0                    parallel-netcdf@1.12.3
  gsl@2.7.1              mgard@2023-12-09               parallelio@2.6.2
  hdf5@1.8.23            mumps@5.6.2                    parmetis@4.0.3
  ==> 464 installed packages
  ```
  :::


- list the installed package you want to know more about

  ```
  spack find openblas
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  -- linux-rhel8-icelake / gcc@12.2.0 -----------------------------
  openblas@0.3.26  openblas@0.3.26

  -- linux-rhel8-icelake / nvhpc@24.5 -----------------------------
  openblas@0.3.26

  -- linux-rhel8-icelake / nvhpc@25.11 ----------------------------
  openblas@0.3.26
  ==> 4 installed packages
  ```
  :::

  more information about it (show difference) 

  ```
  spack find -Lv openblas
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  -- linux-rhel8-icelake / gcc@12.2.0 -----------------------------
  sfcv7zah7u4wzwdlcplnwqmalq6c4fda openblas@0.3.26~bignuma~consistent_fpcsr+dynamic_dispatch+fortran~ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=openmp
  t24jlwiie64odaccv7rfm662p6oa6dnw openblas@0.3.26~bignuma~consistent_fpcsr+dynamic_dispatch+fortran+ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=openmp

  -- linux-rhel8-icelake / nvhpc@24.5 -----------------------------
  w3alzpga4fq43or2nu7763np2dpmiipt openblas@0.3.26~bignuma~consistent_fpcsr+dynamic_dispatch+fortran~ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=openmp

  -- linux-rhel8-icelake / nvhpc@25.11 ----------------------------
  7457aoand3xwgyj5nj6x4cqoqyk6svfz openblas@0.3.26~bignuma~consistent_fpcsr+dynamic_dispatch+fortran~ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=openmp
  ==> 4 installed packages
  ```
  :::

- show what spack did for the package 
  e.g the one
  ```
  sfcv7zah7u4wzwdlcplnwqmalq6c4fda openblas@0.3.26~bignuma~consistent_fpcsr+dynamic_dispatch+fortran~ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=openmp
  ```
  use `/`+ hash
  
  ```
  spack spec /sfcv7zah7u4wzwdlcplnwqmalq6c4fda
  ```
  ::::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  Input spec
  --------------------------------
   -   /sfcv7zah7u4wzwdlcplnwqmalq6c4fda

  Concretized
  --------------------------------
  [^]  openblas@0.3.26%gcc@12.2.0~bignuma~consistent_fpcsr+dynamic_dispatch+fortran~ilp64+locking+pic+shared build_system=makefile symbol_suffix=none threads=openmp arch=linux-rhel8-icelake
  [^]      ^gcc-runtime@12.2.0%gcc@12.2.0 build_system=generic arch=linux-rhel8-icelake
  [e]      ^glibc@2.28%gcc@12.2.0 build_system=autotools arch=linux-rhel8-icelake
  [^]      ^gmake@4.4.1%gcc@8.5.0~guile build_system=generic arch=linux-rhel8-icelake
  [^]          ^gcc-runtime@8.5.0%gcc@8.5.0 build_system=generic arch=linux-rhel8-icelake
  [e]          ^glibc@2.28%gcc@8.5.0 build_system=autotools arch=linux-rhel8-icelake
  [^]      ^perl@5.38.0%gcc@8.5.0+cpanm+opcode+open+shared+threads build_system=generic patches=714e4d1 arch=linux-rhel8-icelake
  [^]          ^berkeley-db@18.1.40%gcc@8.5.0+cxx~docs+stl build_system=autotools patches=26090f4,b231fcc arch=linux-rhel8-icelake
  [^]          ^bzip2@1.0.8%gcc@8.5.0~debug~pic+shared build_system=generic arch=linux-rhel8-icelake
  [^]              ^diffutils@3.10%gcc@8.5.0 build_system=autotools arch=linux-rhel8-icelake
  [^]                  ^libiconv@1.17%gcc@8.5.0 build_system=autotools libs=shared,static arch=linux-rhel8-icelake
  [^]          ^gdbm@1.23%gcc@8.5.0 build_system=autotools arch=linux-rhel8-icelake
  [^]              ^readline@8.2%gcc@8.5.0 build_system=autotools patches=bbf97f1 arch=linux-rhel8-icelake
  [^]                  ^ncurses@6.5%gcc@8.5.0~symlinks+termlib abi=none build_system=autotools patches=7a351bc arch=linux-rhel8-icelake
  [^]                      ^pkgconf@2.2.0%gcc@8.5.0 build_system=autotools arch=linux-rhel8-icelake
  [^]          ^zlib-ng@2.1.6%gcc@8.5.0+compat+new_strategies+opt+pic+shared build_system=autotools arch=linux-rhel8-icelake
  ```

  :::{note}
  - [^] = Existing / already installed (or reused)
  - [e] = External system package
  :::
  
  ::::

- list information about a package which could be installed

  ```
  spack info openblas
  ```
  ::::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  CMakePackage:   openblas

  Description:
      OpenBLAS: An optimized BLAS library

  Homepage: https://www.openblas.net

  Preferred version:
      0.3.26     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.26/OpenBLAS-0.3.26.tar.gz

  Safe versions:
      develop    [git] https://github.com/OpenMathLib/OpenBLAS.git on branch develop
      0.3.26     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.26/OpenBLAS-0.3.26.tar.gz
      0.3.25     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.25/OpenBLAS-0.3.25.tar.gz
      0.3.24     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.24/OpenBLAS-0.3.24.tar.gz
      0.3.23     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.23/OpenBLAS-0.3.23.tar.gz
      0.3.22     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.22/OpenBLAS-0.3.22.tar.gz
      0.3.21     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.21/OpenBLAS-0.3.21.tar.gz
      0.3.20     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.20/OpenBLAS-0.3.20.tar.gz
      0.3.19     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.19/OpenBLAS-0.3.19.tar.gz
      0.3.18     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.18/OpenBLAS-0.3.18.tar.gz
      0.3.17     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.17/OpenBLAS-0.3.17.tar.gz
      0.3.16     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.16/OpenBLAS-0.3.16.tar.gz
      0.3.15     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.15/OpenBLAS-0.3.15.tar.gz
      0.3.14     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.14/OpenBLAS-0.3.14.tar.gz
      0.3.13     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.13/OpenBLAS-0.3.13.tar.gz
      0.3.12     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.12/OpenBLAS-0.3.12.tar.gz
      0.3.11     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.11/OpenBLAS-0.3.11.tar.gz
      0.3.10     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.10/OpenBLAS-0.3.10.tar.gz
      0.3.9      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.9/OpenBLAS-0.3.9.tar.gz
      0.3.8      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.8/OpenBLAS-0.3.8.tar.gz
      0.3.7      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.7/OpenBLAS-0.3.7.tar.gz
      0.3.6      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.6/OpenBLAS-0.3.6.tar.gz
      0.3.5      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.5/OpenBLAS-0.3.5.tar.gz
      0.3.4      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.4/OpenBLAS-0.3.4.tar.gz
      0.3.3      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.3/OpenBLAS-0.3.3.tar.gz
      0.3.2      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.2/OpenBLAS-0.3.2.tar.gz
      0.3.1      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.1/OpenBLAS-0.3.1.tar.gz
      0.3.0      https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.3.0/OpenBLAS-0.3.0.tar.gz
      0.2.20     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.2.20/OpenBLAS-0.2.20.tar.gz
      0.2.19     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.2.19/OpenBLAS-0.2.19.tar.gz
      0.2.18     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.2.18/OpenBLAS-0.2.18.tar.gz
      0.2.17     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.2.17/OpenBLAS-0.2.17.tar.gz
      0.2.16     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.2.16/OpenBLAS-0.2.16.tar.gz
      0.2.15     https://github.com/OpenMathLib/OpenBLAS/releases/download/v0.2.15/OpenBLAS-0.2.15.tar.gz

  Deprecated versions:
      None

  Variants:
      bignuma [false]                 false, true
          Enable experimental support for up to 1024 CPUs/Cores and 128 numa nodes
      build_system [makefile]         cmake, makefile
          Build systems supported by the package
      consistent_fpcsr [false]        false, true
          Synchronize FP CSR between threads (x86/x86_64 only)
      dynamic_dispatch [true]         false, true
          Enable runtime cpu detection for best kernel selection
      ilp64 [false]                   false, true
          Force 64-bit Fortran native integers
      locking [true]                  false, true
          Build with thread safety
      pic [true]                      false, true
          Build position independent code
      shared [true]                   false, true
          Build shared libraries
      symbol_suffix [none]            none
          Set a symbol suffix
      threads [none]                  none, openmp, pthreads
          Multithreading support

      when build_system=cmake
        build_type [Release]          Debug, MinSizeRel, RelWithDebInfo, Release
            CMake build type
        generator [make]              none
            the build system generator to use

      when build_system=cmake ^cmake@3.9:
        ipo [false]                   false, true
            CMake interprocedural optimization

      when @0.3.21:
        fortran [true]                false, true
            w/o a Fortran compiler, OpenBLAS will build an f2c-converted LAPACK

  Build Dependencies:
      cmake  gmake  ninja  perl

  Link Dependencies:
      None

  Run Dependencies:
      None

  Licenses:
      BSD-3-Clause
  ```
  :::{note}
  - @ set version
  - \% set compiler
  - +,~ choose variants with true/false
  - = choose variants with selectable value
  :::
  ::::

- Basic structure of a Spack install spec
  spack install <package>@<version>%<compiler>@<version><variants>^<dependency>
  
  e.g install a older version 0.3.25 of openblas with gcc 12.2.0 

  ```
  spack install openblas@0.3.25%gcc@12.2.0
  ```
  it takes time …
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  [+] /usr (external glibc-2.28-gi6mmtiyx72crixwqwqgtnp3o4syj3n3)
  [+] /usr (external glibc-2.28-u4g25evn3j442btpvqupnzwgdqlwk72i)
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-12.2.0/gcc-runtime-12.2.0-dqfwf7yjtbtdzllj66jx6suk34ir2ct3
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gcc-runtime-8.5.0-tm43bfw5tjxltzb4hh6avyvrxdzodtyb
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/bzip2-1.0.8-ib3znejizupogmu7ontk67drg656svun
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/berkeley-db-18.1.40-wbwxa4xm3pvmc5wzw25ubsqqg5ifcjyv
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gmake-4.4.1-phqmvks6ubh6jf5vhamdtzbmsgqlxsil
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/ncurses-6.5-svfl57usncxqo3ghwesofskr5zm5mgay
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/zlib-ng-2.1.6-jkgunjc2hc2qpkzoodjcn6fu3qpfly73
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/readline-8.2-zeda6mxxdkhdiul5fkfjkgp566et7mqa
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/gdbm-1.23-wiol7vkszckswh2hu34xgtjkgg5p4gve
  [+] /leonardo/prod/spack/06/install/0.22/linux-rhel8-icelake/gcc-8.5.0/perl-5.38.0-jqchh7tmy6sc5ig4xj7cpbhpp55nrgls
  ==> Installing openblas-0.3.25-oicbihueo3lohsnt3vfiphlggy4adpqn [13/13]
  ==> No binary for openblas-0.3.25-oicbihueo3lohsnt3vfiphlggy4adpqn found: installing from source
  ==> Fetching https://mirror.spack.io/_source-cache/archive/4c/4c25cb30c4bb23eddca05d7d0a85997b8db6144f5464ba7f8c09ce91e2f35543.tar.gz
  ==> No patches needed for openblas
  ==> openblas: Executing phase: 'edit'
  ==> openblas: Executing phase: 'build'
  ==> openblas: Executing phase: 'install'
  ==> openblas: Successfully installed openblas-0.3.25-oicbihueo3lohsnt3vfiphlggy4adpqn
    Stage: 1.57s.  Edit: 0.00s.  Build: 7m 8.24s.  Install: 3.18s.  Post-install: 0.37s.  Total: 7m 13.86s
  [+] /leonardo/pub/userexternal/wli00000/spack-0.22.2-06/install/linux-rhel8-icelake/gcc-12.2.0/openblas-0.3.25-oicbihueo3lohsnt3vfiphlggy4adpqn
  ```
  :::

  generate module file for it

  ```
  spack module tcl refresh openblas@0.3.25
  ```
  :::{admonition} output
  :class: dropdown
  show case on Leonardo Booster

  ```
  ==> You are about to regenerate tcl module files for:

  -- linux-rhel8-icelake / gcc@12.2.0 -----------------------------
  oicbihu openblas@0.3.25

  ==> Do you want to proceed? [y/n] y
  ==> Regenerating tcl module files
  ```

  ```
  module avail openblas
  ```
  output:

  ```
  ---------------------- /leonardo/pub/userexternal/wli00000/spack-0.22.2-06/modules ----------------------
  openblas/0.3.25--gcc--12.2.0

  ----------------------------- /leonardo/prod/opt/modulefiles/base/libraries -----------------------------
  openblas/0.3.26--gcc--12.2.0  openblas/0.3.26--nvhpc--24.5  openblas/0.3.26--nvhpc--25.11

  Key:
  default-version  modulepath
  ```
  :::

