FROM jupyter/base-notebook:latest

RUN conda install -c bioconda nextflow\
  && conda clean -afy\
  && find /opt/conda/ -follow -type f -name '*.a' -delete \
  && find /opt/conda/ -follow -type f -name '*.pyc' -delete \
  && find /opt/conda/ -follow -type f -name '*.js.map' -delete
