# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM registry.us-east-1.aliyuncs.com/myk8simages/notebookall:5.7-v3

LABEL maintainer="Jupyter Project <jikun.zhang@qq.com>"

USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    python \
    python-dev \
    python-wheel \
    python-pip && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

#python2

RUN python2 -m pip install --upgrade pip && \
    python2 -m pip install --upgrade setuptools  && \
    python2 -m pip --no-cache-dir install ipykernel matplotlib numpy && \
    python2 -m ipykernel install --user && \
    rm -rf /home/$NB_USER/.local && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

USER $NB_UID

# Install Tensorflow
RUN conda install --quiet --yes \
    'tensorflow=1.11*' \
    'keras=2.2*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Install Tensorflow
RUN conda install --quiet --yes jupyter && \
    conda install --yes -c conda-forge nbgrader && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
