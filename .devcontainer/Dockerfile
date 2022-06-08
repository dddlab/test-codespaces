# See here for image contents: https://hub.docker.com/r/jupyter/datascience-notebook/

FROM jupyter/r-notebook

COPY library-scripts/common-debian.sh /tmp/library-scripts/

USER root

RUN apt-get update \
 && groupadd jovyan \
 && usermod -g jovyan -a -G users jovyan \
 && bash /tmp/library-scripts/common-debian.sh \
 && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts

RUN curl --silent -L --fail \
        https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2021.09.1-372-amd64.deb > /tmp/rstudio.deb && \
    apt-get update && \
    apt-get install -y --no-install-recommends /tmp/rstudio.deb

USER jovyan

RUN pip install \
        jupyter-server-proxy==3.2.0 \
        jupyter-rsession-proxy==2.0.1 && \
    jupyter labextension install @jupyterlab/server-proxy@3.2.0 && \
    jupyter lab build
