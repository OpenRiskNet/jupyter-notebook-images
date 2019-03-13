FROM jupyter/base-notebook:latest

USER 0
RUN apt-get update && apt-get -y install git
USER 1001

RUN conda install rdkit pandas matplotlib cairocffi && conda clean -y -a
