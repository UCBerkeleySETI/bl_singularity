# bl_singularity

[Singularity][] definition files for building containers that are useful for
wsorking with Breakthrough Listen data.

This repository does not contain any pre-built containers.  It only contains the
definition files and various helper files useful for building and deploying the
containers.

The definition files here will likely work with [Apptainer][] as well, but this
is not as throroughly tested.

## Container definitions

This repository includes these subdirectories:

- [`bliss`](bliss): The [Breakthrough Listen Interesting Signal Search][
  bliss_github] tool.

- [`pulsar_container`](pulsar_container): Standard pulsar/postprocessing tools
  often used on BL data.

[Singularity]: https://sylabs.io/singularity/
[Apptainer]: https://apptainer.org
[bliss_github]: https://github.com/n-west/bliss.git