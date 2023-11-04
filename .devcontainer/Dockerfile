FROM rocker/r-ver:4.3 as base
RUN /rocker_scripts/setup_R.sh \
    https://packagemanager.posit.co/cran/__linux__/jammy/2023-09-29
    # https://code.visualstudio.com/docs/devcontainers/create-dev-container#:~:text=Note%3A%20The%20DEBIAN_FRONTEND%20export%20avoids%20warnings%20when%20you%20go%20on%20to%20work%20with%20your%20container.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive 
# RUN apt-get update && apt-get install -y --no-install-recommends \
#     gdebi-core \
#     && rm -rf /var/lib/apt/lists/*
# RUN curl -LO https://quarto.org/download/latest/quarto-linux-amd64.deb
# RUN gdebi --non-interactive quarto-linux-amd64.deb
RUN install2.r --error \
    rhino \
    && rm -rf /tmp/downloaded_packages \
    && strip /usr/local/lib/R/site-library/*/libs/*.so

FROM base as development
# https://www.makeuseof.com/install-python-ubuntu/
# install radian
RUN apt-get update && apt-get -y install software-properties-common  
RUN add-apt-repository -y ppa:deadsnakes/ppa && apt-get update 
RUN apt-get -y install python3.11 python3-pip git
RUN pip3 install radian
# end install radian
RUN install2.r --error \
    languageserver httpgd jsonlite rlang