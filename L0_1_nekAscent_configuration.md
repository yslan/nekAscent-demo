[back to homepage](README.md)

This is a quick go through guide for installing NekRS and Ascent.
In short, it's same as installing NekRS. You don't really need to do anything special for Ascent.
On HPC (Frontier, Aurora and Polaris), simply loading the modules will work.


## Version

- NekRS v24.1, https://github.com/Nek5000/nekRS/tree/v24-development
- Ascent XXX TODO


## Workflow

1. Install NekRS with default modules from `nekrs/scripts`.    
   Ascent is not needed for this so no need to rebuild NekRS if you already have one.

   To recap, on Aurora
   - Get nekrs.      
     Can be at Home or Project Work.
     ```
     git clone https://github.com/Nek5000/NekRS.git nekrs_repo_v24dev
     cd nekrs_repo_v24dev
     git checkout v24-development
     ```

   - Load modules
     ```
     module load cmake
     
     # Not require for compilation, but we use it later
     module use /soft/modulefiles/
     module load ascent/develop/2025-03-19-c1f63e7-openmp
     ```

     As a sanity check, XXX

   - Set target path to installation. Modify it correspondingly.
     ```
     export NEKRS_HOME=/lus/flare/projects/EnergyApps/ylan/.local/nekrs_repo_v24dev
     ```

   - Compile
     ```
     CC=mpicc CXX=mpic++ FC=mpif77 ./build.sh \
              -DCMAKE_INSTALL_PREFIX=${NEKRS_HOME}
     ```

2. Add Ascent env into submit script

   This is already done. Search `USE_ASCENT` in `$NEKRS_HOME/bin/nrsqaub_aurora`.


## Ascent on different machines

### HPC

On `ALCF/Aurora`, `ALCF/Polaris` and `OLCF/Frontier`, the env has been set inside the submit script and can be activaed by `USE_ASCENT=1`.

Basically, one simply has to specify `NEKRS_ASCENT_INSTALL_DIR` for nekrs to link the library at runtime (pre-compilation).
`NEKRS_MPI_THREAD_MULTIPLE=1` is required for async mode. We will talk about it when discussing the performance.

### Local

This is not recommanded in general. Using Docker on Mac could be tricky. Installing Ascent from scratch can easily take an hour.

- Docker    
  See the tutorial from ascent's [doc](https://ascent.readthedocs.io/en/latest/Tutorial_Setup.html)
  
- Install from scratch  
  See the tutorial from ascent's [doc](https://ascent.readthedocs.io/en/latest/QuickStart.html#installing-ascent-and-third-party-dependencies). We only need the CPU/OpenMP backend to run. GPU is not required.

