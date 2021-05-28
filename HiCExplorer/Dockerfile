FROM python:3

WORKDIR /usr/src/app

#COPY requirements.txt ./
#RUN pip install --no-cache-dir -r requirments.txt

#COPY . .

RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/deeptools/HiCExplorer/archive/refs/tags/3.6.tar.gz

RUN tar -xzvf 3.6.tar.gz

RUN cd HiCExplorer-3.6 && python setup.py install

#RUN cd HiCExplorer-3.6 && pip install --no-cache-dir -r requirements.txt

COPY requirements-noPython.txt .

RUN pip install --no-cache-dir -r requirements-noPython.txt


ENTRYPOINT bash

