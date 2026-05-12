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

- mylib: [click to download]()

  mylib is library contains only 1 function of naive matrix multiplication {math}`C_{ij} = \sum_k A_{ik} \times B_{kj} + C_{ij}`

  ```
  mylib
  ├── include
  │   └── mymath.h
  └── src
      └── mymath.c
  ```

- myapp: [click to download]()
  
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
  - compiler flag `-O`
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

- check out the make branch of mylib

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

- check out the make branch of myapp

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
  ```

  ```
  module avail myapp
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
