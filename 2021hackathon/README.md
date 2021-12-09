# Creating Standard Software Container Infrastructure

Software containers (e.g., docker or singularity) have become an essential tool in providing reproducible and portable scientific applications. Containers encapsulate linux software installations in an overlay filesystem that can be used to execute custom software. For instance, we have built containers to run R, Rstudio, python and other specific application environments. Several additions can significantly improve the reliability and effort required for building out additional containers within a Docker framework.

- Standard build process: currently MCC scientific computing uses the EZbuild system to compile and install cluster software packages. Incorporating EZbuild recipes into the container-building process would reduce duplication of effort and leverage MCC IT expertise.

- Standard build hierarchy: many research applications require a complex software stack (e.g., python, latex) using a specific OS (e.g., ubuntu, centos). The standard approach for building containers in these cases involves developing a base image (e.g., an OS) followed by additional containers extending functionality. Defining the hierarchy of containers (e.g., OS, programming languages, application environments) will allow us to quickly add new containers, leveraging previously built containers.

- MCC-specific container customization: several MCC-specific modifications are required to run containers, including SSL-inspection and portability to singularity. Containers should be tested against singularity to ensure correct operation. 4) Implementation of specific genomics/proteomics containers: develop containers (and container versioning) for specific software tool such as gatk, genome annotation, STAR, etc.

Impact: The result of this effort will be a series of gitlab-versioned Dockerfiles that generate container images stored in a new local Dockerhub instance. The dockerfiles and docker images will be available to the MCC community to use within their research, with particular emphasis on use on the MCC HPC environment. Documentation about container development conventions and versioning will be included in the gitlab project(s).

Technical Specifications: Linux, docker/singularity, software installation

Programming background: Shell scripting, familiarity with linux OS commands and installation.
