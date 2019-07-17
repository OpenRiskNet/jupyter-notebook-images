FROM jupyter/base-notebook:latest

RUN conda install --yes --freeze-installed rdkit pandas matplotlib cairocffi\
  && conda clean -afy\
  && find /opt/conda/ -follow -type f -name '*.a' -delete \
  && find /opt/conda/ -follow -type f -name '*.pyc' -delete \
  && find /opt/conda/ -follow -type f -name '*.js.map' -delete
