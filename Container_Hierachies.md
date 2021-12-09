# Creating Container Hierachies

The purpose of this file is to document the options for container hierarchies, links to work done on this topic and potential experiments that are performed to understand the options.

## Problem Definition
Caveat: it should be noted that container hiearchies for our purposes reflect the needs for scientific computing within a cancer center. So it is very specific to a set of use cases.

Our center has specific environmental considerations that may make it more difficult to de-novo use a container from the internet. Therefore, we want to better understand how to build containers without having to duplicate work as much as possible. For containers, one can start with a base image and add software to it. The question is whether or not there is an optimal (or semi-optimal) hierachy of containers to build up that would make the process as easy as possible for subsequent builds. That is, does something like
```
base_os -> local_environment |-> c compiler |-> R

                             |-> java -> gatk
```


## Docker Size
One classic conflict with docker and science, is the standard practice of minimizing the container size:

https://docs.docker.com/develop/develop-images/dockerfile_best-practices/

Some of the tools we use require many different packages to get installed. For instance, in the case of R, we often build R from scratch which then requires gcc and other tools.

- One option would be to install the build tools, install the application, then uninstall the build tools. This may be fairly complex to configure but would significant reduce the image size.

- One option for managing the complexity of lots of different packages would be in the style of https://laradock.io/

## Base OS
What is the right OS to use as a base operating system? 
- Basic with certs (alpine, unbuntu?)
- Basic + R (compile from scratch
- Basic + 
