# Maxquant

# Using the Container
Several versions of the container may be available. However, the general structure is as follows:

The MaxQuant binary (and supporting files) are installed in /opt/MaxQuant_version with a symlink made for /opt/MaxQuant.

The entrypoint is /opt/MaxQuant/bin/MaxQuantCmd.exe (meaning if you do not specify a command, this is executed).

The XML file that drives a maxquant analysis is complicated and perhaps best configured using the MaxQuant software (in Windows). However, you can generate a template file using
```
docker run -v `pwd`:/data dockerhub.moffitt.org/hpc/maxquant:2.0.3.1 --create /data/template.xml
```
NOTE: the reason for the `-v` flag is that nothing is mounted by default in the container, so you cannot write the output anywhere.

or

```
singularity run docker://dockerhub.moffitt.org/hpc/maxquant:2.0.3.1 --create template.xml
```
NOTE: Running this from your home directory means that your home dir is mounted so this will create the file in your home directory.

# Drive mapping
There are no explicit paths required within the container. However, nothing is mounted by default in the container therefore maxquant will need access to the .RAW files, xml file and uniprot annotation files. The xml file is referred to in the command line and all other files are included in the xml file.

My suggestion is as follows. Assume that your protein data is in `/share/lab_mylab/proteomics/experiment1`. 

In the XML file (ideally in the root of the `experiment1` directory), refer to the path `/share/lab_mylab/proteomics/experiment1` for input files, etc. 

The command to run would be:
```
singularity run --bind /share/lab_mylab docker://dockerhub.moffitt.org/hpc/maxquant:2.0.3.1 /share/lab_mylab/proteomics/experiment1/MaxQuant_mqpar.xml
```

You can, of course, put the uniprot files in the same experiment directory. However, these may not change much and so should be stored in a more general directory. Let's assume that's in `/share/annotation_files/uniprot_vXYZ`.  In the XML file, refer to the annotation file using this path. Then, the command to run will be:
```
singularity run --bind /share/lab_mylab,/share/annotation_files docker://dockerhub.moffitt.org/hpc/maxquant:2.0.3.1 /share/lab_mylab/proteomics/experiment1/MaxQuant_mqpar.xml
```

# Other Notes

Some notes on maxquant and the maxquant container.

- The parallel nature of maxquant appears to be implemented per file (see https://sciwiki.fredhutch.org/compdemos/maxquant/ for this implied behavior). This should be verified.
- There is a script (https://github.com/atc3/maxquant_linux_guide) that looks interesting for managing a series of xml templates (for common runs). This could be used to merge templated settings with specific files for an experiment.
