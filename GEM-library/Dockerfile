FROM amd64/ubuntu:22.10

WORKDIR /opt

RUN apt-get -y update && apt-get -y install \
    tar \
    lbzip2

COPY ./GEM-binaries-Linux-x86_64-core_i3-20130406-045632.tbz2 .

RUN tar -xf GEM-binaries-Linux-x86_64-core_i3-20130406-045632.tbz2

ENV PATH=/opt/GEM-binaries-Linux-x86_64-core_i3-20130406-045632/bin:$PATH

CMD [gem-mappability]
