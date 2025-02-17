# rMD-autoencoder
Reinforced molecular dynamics: Physics-infused generative machine learning model simulates protein motion
## Released under MIT License

## Copyright (c) 2025 Istvan B Kolossvary.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

### Please cite this publication in any work where you use our software or its derivatives...

### This GitHub repository contains all the code and data to reproduce the results in... There are 3 top directories, 'Simulations' for running the MD simulations, 'Autoencoder' to train and make predictions with the rMD Autoencoder, and 'Refinement' to refine the ML-predicted protein structures. Each sub-directory contains README files with detailed instructions and explanations of the contents of that directory.

### 1. meta-eABF MD simulations:
To run the simulations one needs to install OpenMM-PLUMED. The best way of installing OpenMM and its plugin to work with PLUMED is via conda. Assuming one has a recent Anaconda3 installation:

    conda create -n openmm-plumed-drr
    conda install conda-forge::openmm-plumed
    conda activate openmm-plumed-drr
    conda remove --force plumed

The last step is crucial. The built-in plumed does not have the necessary modules included. One has to remove it and install PLUMED separately from source as detailed on the PLUMED website. When it comes to the configure step use the following options:

./configure --prefix=/where/you/install/plumed CXXFLAGS=-O3 --enable-boost_serialization --enable-mpi --enable-openmp --enable-modules=drr

At this point one can run OpenMM-PLUMED jobs but has to tell the OpenMM-PLUMED plugin where to find the PLUMED libraries.

    conda activate openmm-plumed-drr
    export LD_LIBRARY_PATH=/where/you/install/plumed/lib:$LD_LIBRARY_PATH
    export PATH=/where/you/install/plumed/bin:$PATH

The user need not actually run the simulations to experiment with the results, the trajectories and the free energy map of the 2 us simulations are included in this directory.

### 2. rMD Autoencoder computations:
To run the computations the user needs Wolfram/Mathematica 14.1 or higher. The notebook refers to data in the Simulations directories and it requires a reasonablty strong Linux desktop computer with a recent nVidia GPU and 32 GB or more RAM.

I also provided a version of the notebook that can be interactively viewed with the free Wolfram Player with limited functionality.

I also included a static PDF version of the notebook.

### 3. Structure refinement:
To run the relaxation protocols, the user needs either the Rosetta-Relax software or it can be run without any softwer using the ROSIE server. The final position restrained minimization protocol requires the free AmberTools software, which can be installed, e.g., via 'conda install conda-forge::ambertools'
