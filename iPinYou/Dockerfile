FROM rocker/r-base:latest
MAINTAINER Wush Wu <wush978@gmail.com>

RUN apt-get update
RUN apt-get install -y libpq-dev libmysqlclient-dev libgit2-dev libxml2-dev libcurl4-openssl-dev
RUN useradd -ms /bin/bash wush
USER wush
WORKDIR /home/wush
ENV R_LIBS_USER /home/wush/R
RUN mkdir -p /home/wush/R
RUN echo "options(repos='http://cran.csie.ntu.edu.tw')"
RUN Rscript -e "install.packages(c('RPostgreSQL', 'RMySQL', 'dplyr', 'RSQLite', 'devtools'))"
RUN Rscript -e "devtools::install_github('macrodatalab/BigObjectRPkgs', subdir = 'RBigObject')"
