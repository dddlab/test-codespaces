FROM jupyter/r-notebook:2022-06-20

USER root

RUN curl --silent -L --fail \
        https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2022.02.3-492-amd64.deb > /tmp/rstudio.deb && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        /tmp/rstudio.deb lmodern && \
    apt-get clean -y && \
    rm -rf /tmp/rstudio.deb /var/lib/apt/lists/* /tmp/library-scripts

USER ${NB_UID}

RUN pip install --no-cache-dir \
        jupyter-server-proxy==3.2.1 \
        jupyter-rsession-proxy==2.0.1 && \
    jupyter labextension install @jupyterlab/server-proxy@3.2.1 && \
    jupyter lab build

COPY --chown="${NB_UID}:${NB_GID}" library-scripts/get-rstudio-url.sh /opt/conda/bin/