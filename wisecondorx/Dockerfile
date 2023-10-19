FROM --platform=linux/amd64 ubuntu:22.04

WORKDIR /opt

## Install required packages for python installation
RUN apt-get update && apt-get install -y wget \
    git \
    build-essential \
    zlib1g-dev \
    libncurses5-dev \
    libgdbm-dev \
    libnss3-dev \
    libssl-dev \
    libreadline-dev \
    libffi-dev \
    libsqlite3-dev \
    libbz2-dev

## Install python
ENV PYTHON_VERSION=3.6.8
RUN wget --quiet https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz \
    && tar -xzf Python-${PYTHON_VERSION}.tgz \
    && cd Python-${PYTHON_VERSION} \
    && ./configure --enable-optimizations \
    && make altinstall

## Install required packages - as listed on github
COPY requirements.txt .
RUN pip3.6 install -r requirements.txt

## Install modified WisecondorX package
RUN pip3.6 install -U git+https://github.com/PMCC-CancerGenomicsTRC/WisecondorX


## Install R
ENV R_VERSION=3.4.0

## Set up environment to work around timezone prompts from R installation
ENV TZ=Australia/Melbourne
RUN echo "Australia/Melbourne" > /etc/timezone
RUN echo "Australia/Melbourne" > /etc/localtime

RUN apt-get update && apt-get install -y gdebi-core \
    && wget --quiet https://cdn.rstudio.com/r/ubuntu-2204/pkgs/r-${R_VERSION}_1_amd64.deb \
    && gdebi -n r-${R_VERSION}_1_amd64.deb \
    && ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R \
    && ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript

## Install required packages - as listed on github
RUN wget --quiet https://bioconductor.org/packages/3.5/bioc/src/contrib/DNAcopy_1.50.1.tar.gz \
    && R CMD INSTALL DNAcopy_1.50.1.tar.gz \
    && wget --quiet https://cran.r-project.org/src/contrib/Archive/jsonlite/jsonlite_1.5.tar.gz \
    && R CMD INSTALL jsonlite_1.5.tar.gz
