# First Example

[back to homepage](README.md)

Here, we will go through a simple example to explain how `nekAscent` works.

## Run the example

This is a modified NekRS `turbPipePeriodic` example, `tpp` for short.

https://drive.google.com/file/d/1l2oN64Br0JdKoTk1yAWAT-LlfqbZ43nY

`<REPLACE>`

- example0_turbPiperPeriodic

0. Get the example

   ```
   cd ex01_pipe
   tar zxvf pipe.re2.tar.gz
   ```

   We will kick start the simulation using a fully developed flow profile from
   the restart file [google drive](https://drive.google.com/file/d/1l2oN64Br0JdKoTk1yAWAT-LlfqbZ43nY/view).
   One could try this command to download it:
   ```
   wget "https://drive.usercontent.google.com/download?id=1l2oN64Br0JdKoTk1yAWAT-LlfqbZ43nY&confirm=t" -O turbPipePeriodic_re19k_t40_N9_r3v.fld
   ```

1. Pre-check

   1. In UDF, make sure `#include "nekAscent.hpp"` is uncommented.

   2. In par file, read the checkpoint file `startFrom = "turbPipePeriodic_re19k_t40_N9_r3v.fld"`

   3. Create the folder for incoming images
      ```
      mkdir -p imgs
      ```

2. Run the example

   Ascent is linked only when the UDF is compiled (at pre-compilation)

   ```
   # Change project id and queue correspondingly
   USE_ASCENT=1 PROJ_ID=EnergyApps QUEUE=debug $NEKRS_HOME/bin/nrsqsub_aurora pipe 1 00:30
   ```

3. Post-checks 

   XXX: log, img, scripts from png to gif


## Step-by-Step Breakdown

Following this, you will be able to set up a basic case from zero.
Then, it's time to try your own cases!

- UDF

- Ascent actions: `ascent.yml`

- logfile analysis


## Other things to try

Start with the Scenes.
- Change resolution
- Add a new image to plot pressure
- Add a slice into image
- Change colormap, cmin and cmax
- Camera orientation
- Annotation

Next, try adding a pipeline into scene
- velocity magnitude
- contour lines

Next, combos

We will showcase some commonly used features in the live demo. 
Bring your own quest!



