FROM jupyter/base-notebook:latest

RUN conda install rdkit pandas matplotlib cairocffi && conda clean -y -a

USER 0
RUN apt-get update && apt-get -y install git
USER 1001
