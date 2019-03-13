FROM jupyter/base-notebook:latest

RUN apt-get update && apt-get -y install git

RUN conda install rdkit pandas matplotlib cairocffi && conda clean -y -a
