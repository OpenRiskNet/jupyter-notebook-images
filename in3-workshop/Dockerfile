FROM jupyter/datascience-notebook:3deefc7d16c7

USER root

# R pre-requisites
RUN apt-get clean && \
    mv /var/lib/apt/lists /tmp && \
    mkdir -p /var/lib/apt/lists/partial && \
    apt-get clean && \
    apt-get update --allow-unauthenticated && \
    apt-get install -y --no-install-recommends \
        fonts-dejavu \
        gfortran \
        build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

RUN conda install --yes --freeze-installed \
    pandas \
    requests \
    simplejson \
    ipywidgets \
    seaborn \
    matplotlib \
    r-pheatmap \
    r-reshape2 \
    r-gplots \
    r-rcolorbrewer \
    r-ggplot2 \
    r-biocmanager \
    r-drc \
  && conda clean -afy\
  && find /opt/conda/ -follow -type f -name '*.a' -delete \
  && find /opt/conda/ -follow -type f -name '*.pyc' -delete \
  && find /opt/conda/ -follow -type f -name '*.js.map' -delete \
  && fix-permissions $CONDA_DIR \
  && fix-permissions /home/$NB_USER \
  && fix-permissions /etc/jupyter/

RUN R -e 'BiocManager::install("DESeq2")' && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER && \
    fix-permissions /etc/jupyter/

USER $NB_USER
