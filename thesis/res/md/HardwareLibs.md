## Building
User can build libraries separately or as one project. In both cases, out-of-source building is supported.

### Building whole project
To build all libraries at once, use the following commands:

 * `git clone ssh://git@gitlab.cern.ch:7999/atlas-trt-dcs-ggss/ggss-hardware-libs.git` to clone the repository from GitLab

 * `mkdir <build_directory` where *build_directory* should be CMake output directory

 * `cd ggss-hardware-libs`

 * `git submodule update --init --recursive --remote`

 * `cd ../<build_directory>`

 * `cmake ../ggss-hardware-libs` 

 * `make`

You can also use the following *one-liner*:

`git clone ssh://git@gitlab.cern.ch:7999/atlas-trt-dcs-ggss/ggss-hardware-libs.git && mkdir ggss-hardware-libs-build && cd ggss-hardware-libs && git submodule update --init --recursive --remote && cd ../ggss-hardware-libs-build && cmake ../ggss-hardware-libs && make`
