# nekAscent Demo     

Underconstruction!
Underconstruction!
Underconstruction!

This will be a self-guided tutorial run insitu visualization using NekRS + Ascent.

NekRS version: v24-development, https://github.com/Nek5000/nekRS/tree/v24-development

## Prerequisite

- (Required) Experience in installing and running NekRS.
- (Preferred) Experience with and access to HPC systems (ALCF/Aurora will be used in the demo).
- (Optional) Some experience in Docker (or CMake) if one wants to run locally.
- Go through the lessons 0.1 and 0.2 by yourself.

## Lessons

<style>
  /* Zerobased hierarchical numbering: 0., 0.1., 0.2., 1., 1.1., ... */
  ol.zerobased {
    counter-reset: item -1;           /* start top-level at 0 (first increment -> 0) */
    list-style: none;                 
    padding-left: 1.8em;              /* space for the generated numbers */
  }
  ol.zerobased li {
    position: relative;
    margin: 0.25em 0;
  }
  ol.zerobased li::before {
    counter-increment: item;          /* bump the current level counter */
    content: counters(item, ".") ". ";/* full path like 0.1. */
    position: absolute;
    left: -1.8em;                     /* align numbers to the left gutter */
    width: 1.6em;
    text-align: right;
  }
  /* Each nested <ol> starts a new counter scope at this level */
  ol.zerobased ol {
    list-style: none;
    padding-left: 1.8em;
    counter-reset: item;              /* inner levels start at 1 (default) */
  }
</style>


<ol class="zerobased">
  <li>Intro item (numbered 0.)</li>
    <ol>
      <li>(DIY) Configuration / Installation: 
        <a href="L0_1_nekAscent_config.md" target="_blank" rel="noopener">L0.1&nbsp;Link</a>
      </li>
      <li>(DIY) Run an example:
        <a href="L0_2_run_an_example.md" target="_blank" rel="noopener">L0.2&nbsp;Link</a>
      </li>
    </ol>
  </li>
</ol>


<!-- renders as 1.2. ccc 
- 0.1 (DIY) Configuration / Installation: [L0.1 Link](L0_1_nekAscent_config.md)

- 0.2 (DIY) Run an example: [L0.2 Link](L0_2_run_an_example.md)
-->

1. Introduction -- Capabilities and Workflow        

  (TODO slides)

2. Hands-on -- How To XYZ

   - 2a. Ascent
   
     - Clip
     - Isosurface
     - Show Mesh
     - Velocity Magnitude
     - Reuse Pipeline
     - Volume Rendering
     - Colormap
     - Camera View
   
   - 2b. NekRS usecase
   
     - performance: monitor and improvement
     - plot CFL
     - qcriterion, lambda2
     - debugging simulation
     - neknek

3. (Appendix) Big Files        

     - png to mp4
     - mp4 editor
     - YouTube upload

4. Features Survey

     - Ascent installation workthrough guide / video?
     - multiple ascent files
     - default imgs path?
     - performance: CPU pinning
     - particles, trace and streamline
     - ray tracing
     - build-in fields
     - add option to edit actions after reading ascent.yml to rescale colormap from the solver


### Resources

Ascent

- Github
  https://github.com/Alpine-DAV/ascent

- Discussion
  https://github.com/Alpine-DAV/ascent/discussions

- Documentation
  https://ascent.readthedocs.io/en/latest/index.html

- VisIt Session Converters
  https://github.com/Alpine-DAV/ascent/tree/develop/src/utilities/visit_session_converters

- Tutotials
  https://ascent.readthedocs.io/en/latest/Tutorial.html

- SC23 Tutorial
  https://github.com/Alpine-DAV/sc23-tutorial

Gallery


### Credit

