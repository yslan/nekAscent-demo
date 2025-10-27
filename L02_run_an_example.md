# First Example

[back to homepage](README.md)

Here, we will go through a simple example to explain how `nekAscent` works.

## Run the example

This is a modified NekRS `turbPipePeriodic` example.

0. Get the example

   ```
   cd ex02_pipe
   tar zxvf pipe.re2.tar.gz
   ```

   We will kick start the simulation using a fully developed flow from the
   restart file [google drive](https://drive.google.com/file/d/1l2oN64Br0JdKoTk1yAWAT-LlfqbZ43nY/view).
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

   It's the same way to submit a job via script but with `USE_ASCENT=1` to
   activate the related environment.
   
   ```
   # Change project id and queue correspondingly
   USE_ASCENT=1 PROJ_ID=EnergyApps QUEUE=debug $NEKRS_HOME/bin/nrsqsub_aurora pipe 1 00:30
   ```

3. Post-checks 

   Ascent is linked only when the UDF is compiled (at pre-compilation)     
   XXX: log, img, scripts from png to gif
   show some output images here


## Step-by-Step Breakdown

Following this, you will be able to set up a basic case from zero.
Then, it's time to try your own cases!

- UDF

  0. **On/off switch**.  
     The preprocessor macro `NEKRS_ASCENT_ENABLED` is defined in `nekAscent.hpp`.
     To toggle the extra nekAscent settingsm comment or uncomment the 
     `#include "nekAscent.hpp"` line. Search for the macro in your UDF to locate
     the plugin-specific code.

  1. (`UDF_Setup`) `nekAscent::addVariable`

     Following other NekRS interface, a field can be passed to nekAscent via
     `std::vector<deviceMemory<dfloat>>`. Here, we send the pointer of
     velocity components and register the name as "velocity" (can be arbitrary).
     ```
     nekAscent::addVariable("velocity", mesh, o_U);
     ```

  2. (`UDF_Setup`) `nekAscent::setup`

     User specify the `mesh` of the field in case of having a solid domain followed
     by the Ascent action file "ascent.yaml". The rest arguments are optional.

     ```
     const int Nviz = 13;            // polynomial order used in visualization
     const auto uniform = true;      // uniform grid or Gauss-Lobatto points
     const auto stageThroughHost = true; // works on my laptop and frontier
     const auto async = true;        // asyncronization mode, it's faster on Frontier
     nekAscent::setup(mesh, "ascent.yaml", Nviz, uniform, stageThroughHost, async);
     ```
  3. (`UDF_ExecuteStep`) `nekAscent::run`

     We use the variable `ioStepAscent` (customized par key, passed in `UDF_Setup`)
     to control how frequent Ascent is called. 
     ```
     nekAscent::run(time, tstep);
     ```
     Each time, the "ascent.yaml" will be read again allowing user to adjust the
     visualzation at runtime. See `turbPipe` example for a more sophiscated usage.

- Ascent actions: `ascent.yml`

  - Pipelines.    
    A pipeline defines a sequence of geometric filters. Ascent provides many
    filters (see the [doc-filter](https://ascent.readthedocs.io/en/latest/Actions/Pipelines.html#filters)
    )

    In this example:
    - `pl1`: slice at `x=1e-4` 
    - `pl2`: slice at `y=0`
    - `pl5`: first slice at `x=-1e-4`, then clip with the plane `y=0` to produce
      a yz half plane.
    - `pl6`: first slice at `y=-1e-4`, then clip with the plane `x=0` to produce
      a xz half plane.
    - `pl7`: slice at `z=7.4`

  - Scenes.    
    A scene generates images: you specify which field to plot, which pipeline
    to use, and the rendering parameters.

    - `s1`: plot `vz` on `pl1` using "Cool to Warm Extended" colormap
      (see the [doc-colormap](https://ascent.readthedocs.io/en/latest/Actions/VTKmColorTables.html#vtk-m-color-tables))
      with colors values clipped to [-0.5,1.5]. Outputs are saved as
      `imgs/vz_xslice_%06d` in the `imgs` folder we created at a resoluation of
      `2048 x 256` pixels.

    - `s2`: plot `vz` on `pl2`. showcasing an alternative way to specify the
      camera position. Outputs are saved as `imgs/vz_yslice_%06d`.

    - `s3`: plot three pipelines `pl5`, `pl6` and `pl7` with `vz`. Outputs are
       saved as `imgs/vz_3slices_%06d`.

    Other than pseudocolor, one can also plot mesh (Nvis grid, not spectral
    element) or volume.

- logfile analysis


## Other things to try

Start with the Scenes:
- Change resolution. Say we want 4k images.
- Familiar with camera option.
- Change colormap, cmin and cmax. [doc-colormap](https://ascent.readthedocs.io/en/latest/Actions/VTKmColorTables.html#vtk-m-color-tables)
- Annotation. See [doc-render](https://ascent.readthedocs.io/en/latest/Actions/Scenes.html#additional-render-options) for more options.

Pipeline:
- Try some other filter. [doc-filter](https://ascent.readthedocs.io/en/latest/Actions/Pipelines.html#filters). For example, composite velocity magnitude and get isosurfaces.

UDF API:
- Pass `pressure` via `addVariable` and plot it on some of the pipelines.

We will showcase some commonly used features in the live demo. 
Bring your own quest!

