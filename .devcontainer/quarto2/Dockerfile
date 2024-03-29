# See here for image contents: https://hub.docker.com/r/jupyter/datascience-notebook/

FROM jupyter/datascience-notebook

# We want to run common-debian.sh from here:
# https://github.com/microsoft/vscode-dev-containers/tree/main/script-library#development-container-scripts
# But that script assumes that the main non-root user (in this case jovyan)
# is in a group with the same name (in this case jovyan).  So we must first make that so.
COPY library-scripts/common-debian.sh /tmp/library-scripts/
USER root
RUN apt-get update \
 && groupadd jovyan \
 && usermod -g jovyan -a -G users jovyan \
 && bash /tmp/library-scripts/common-debian.sh \
 && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts

# Get rid of TeXLive. It's old
RUN apt-get autoremove --purge --yes texlive tex-common

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    gdebi-core \
    && rm -rf /var/lib/apt/lists/*

RUN curl -LO https://github.com/quarto-dev/quarto-cli/releases/download/v1.1.251/quarto-1.1.251-linux-amd64.deb
RUN gdebi --non-interactive quarto-1.1.251-linux-amd64.deb

USER jovyan

RUN quarto install tool tinytex

RUN PATH=/home/jovyan/.TinyTeX/bin/x86_64-linux:$PATH

