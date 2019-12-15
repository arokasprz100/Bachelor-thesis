## Using BuildDependencies.cmake template
To use this template:

 * add path to the template to **CMAKE_MODULE_PATH** variable

 * define **target_name** CMake variable - it should contain name of existing CMake project - built dependencies will be linked to it

 * define **BUILD_OUTPUT_DIRECTORY** variable - it should contain path to directory where build output will be placed - is using this template
 with *BuildLibrary.cmake*, this variable is defined there - it is set to directory CMake was called from

 * define **dependencies** variable - it should contain list of paths to dependencies that should be built. Omit *-lib* suffix - all GGSS libraries 
 contain it, so it is added by the template itself 

 * define **dependency_prefix** variable - it should contain common part of all dependencies paths


Example usage:
```cmake
# Set target_name variable
set(target_name "ggss")

# Add template path to CMAKE_MODULE_PATH variable
set(ggss_misc_path 
    "${CMAKE_CURRENT_SOURCE_DIR}/ggss-software-libs/ggss-util-libs/ggss-misc")
list(APPEND CMAKE_MODULE_PATH "${ggss_misc_path}/cmake_templates")

# Include BuildLibrary.cmake template - it sets BUILD_OUTPUT_DIRECTORY variable
include(BuildLibrary)

# Set dependency_prefix variable - path to every dependency will start with it.
set(dependency_prefix "${CMAKE_CURRENT_SOURCE_DIR}")

# Define list of dependencies - omit '-lib' suffix
set(dependencies "ggss-hardware-libs/ortecmcb" 
    "ggss-hardware-libs/caenhv" 
    "ggss-hardware-libs/usbrm"
    "ggss-software-libs/fit"
    "ggss-software-libs/xml"
    "ggss-software-libs/fifo" )

# Include template itself
include(BuildDependencies)

```

<div style="page-break-after: always;"></div>

## Using BuildLibrary.cmake template
To use this template:

 * add path to the template to **CMAKE_MODULE_PATH** variable
 
 * define **target_name** CMake variable - it should contain name of library that should be build (without any lib prefix/suffix)

Example usage:
```cmake
# Set target_name variable
set(target_name "log")

# ...

## # Add template path to CMAKE_MODULE_PATH variable
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/../ggss-misc/cmake_templates")

# Include template itself
include(BuildLibrary)

# ...

```
