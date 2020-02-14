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
    rm -rf /var/lib/apt/lists/* && \
    chmod g+w /etc/passwd
# we make /etc/password writeable by group so that when we run as non-root user it can be added and we get a username

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
    r-mass \
    r-rjsonio \
    r-dplyr \
    r-magrittr \
  && R -e 'BiocManager::install("DESeq2")' \
  && conda clean -afy\
  && find /opt/conda/ -follow -type f -name '*.a' -delete \
  && find /opt/conda/ -follow -type f -name '*.pyc' -delete \
  && find /opt/conda/ -follow -type f -name '*.js.map' -delete \
  && chgrp -Rf root $CONDA_DIR \
  && chmod -Rf g+rwX $CONDA_DIR \
  && chgrp -Rf root /home/$NB_USER \
  && chmod -Rf g+rwX /home/$NB_USER \
  && chgrp -Rf root /etc/jupyter/ \
  && chmod -Rf g+rwX /etc/jupyter/

USER $NB_USER
