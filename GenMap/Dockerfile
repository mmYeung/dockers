FROM amd64/ubuntu:22.10

RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    cmake \
    make \
    gcc \
    clang \
    libseqan2-dev \
    git \
    libomp-dev

WORKDIR /opt

RUN wget https://github.com/cpockrandt/genmap/archive/refs/tags/genmap-v1.3.0.zip && unzip genmap-v1.3.0.zip

RUN mv genmap-genmap-v1.3.0 genmap_v1.3.0

WORKDIR /opt/genmap_v1.3.0

RUN cmake . -DCMAKE_BUILD_TYPE=Release

RUN make genmap

RUN make install

ENTRYPOINT ["genmap"]
