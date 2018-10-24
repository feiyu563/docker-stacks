# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM registry.us-east-1.aliyuncs.com/myk8simages/notebookall:5.7-v4

LABEL maintainer="Jupyter Project <jikun.zhang@qq.com>"

USER root

# RSpark config
ENV R_LIBS_USER $SPARK_HOME/R/lib
RUN fix-permissions $R_LIBS_USER

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    tzdata \
    python \
    python-dev \
    python-wheel \
    python-pip \
    gfortran \
    gcc && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID
#tf
RUN conda install --quiet --yes \
    'tensorflow=1.11*' \
    'keras=2.2*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
    
# R packages
RUN conda install --quiet --yes \
    'r-base=3.4.1' \
    'r-irkernel=0.8*' \
    'r-ggplot2=2.2*' \
    'r-sparklyr=0.7*' \
    'r-rcurl=1.95*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Apache Toree kernel
RUN pip install --no-cache-dir \
    https://dist.apache.org/repos/dist/dev/incubator/toree/0.3.0-incubating-rc1/toree-pip/toree-0.3.0.tar.gz \
    && \
    jupyter toree install --sys-prefix && \
    rm -rf /home/$NB_USER/.local && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
    
#python2

RUN python2 -m pip --no-cache-dir install ipykernel matplotlib numpy && \
    python2 -m pip install --upgrade pip && \
    python2 -m pip install --upgrade setuptools  && \
    python2 -m ipykernel install --user && \
    rm -rf /home/$NB_USER/.local && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
    
# Spylon-kernel
RUN conda install --quiet --yes 'spylon-kernel=0.4*' && \
    conda clean -tipsy && \
    python -m spylon_kernel install --sys-prefix && \
    rm -rf /home/$NB_USER/.local && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
