## Remember to build with --platform linux/amd64
FROM python:3.12

WORKDIR /opt

## Install bwa to ensure that the "extract" function works
RUN apt-get update && apt-get install -y bwa

RUN git clone --recursive https://gitlab.com/vincent-sater/umi-varcal && \
    cd umi-varcal && \
    git checkout e4b80530a30ba07740c21238e4f9e9f8e629eeb9

RUN rm umi-varcal/functions/functions.c umi-varcal/functions/functions.cpython-310-x86_64-linux-gnu.so

## Note: pyfasta setuptools psutil packages are missing from the README of the gitlab
RUN pip install cython msgpack==0.6.2 pyfaidx pyfasta pysam scipy statsmodels setuptools psutil
RUN cd umi-varcal/functions && python3 setup.py build_ext --inplace

## sed commands below are required to adjust code in deprecated package pyfasta to ensure that functions etc are loaded from the correct location/updated package names
RUN sed -i "s/from fasta/from pyfasta.fasta/;s/from records/from pyfasta.records/;s/from split_fasta/from pyfasta.split_fasta/" /usr/local/lib/python3.12/site-packages/pyfasta/__init__.py

RUN sed -i "s/from collections/from collections.abc/;s/from records/from pyfasta.records/" /usr/local/lib/python3.12/site-packages/pyfasta/fasta.py

RUN sed -i "s/import cPickle/import pickle/" /usr/local/lib/python3.12/site-packages/pyfasta/records.py

RUN sed -i "s/from cStringIO/from io/" /usr/local/lib/python3.12/site-packages/pyfasta/split_fasta.py

# RUN sed -i 's/pileup = msgpack\.unpack(handle, encoding="utf-8", max_buffer_size=100\*1024\*1024\*1024)/pileup = msgpack.unpack(handle, raw=False, strict_map_key=False)/' umi-varcal/functions/functions.pyx
# RUN sed -i 's/msgpack\.pack(pileup, handle, encoding="utf-8")/msgpack.pack(pileup, handle)/' umi-varcal/functions/Call.py

# RUN sed -i 's/pileup = msgpack\.unpack(handle, encoding="utf-8")/pileup = msgpack.unpack(handle, raw=False, strict_map_key=False)/' umi-varcal/functions/functions.pyx


ENTRYPOINT [ "python", "/opt/umi-varcal/umi-varcal.py" ]