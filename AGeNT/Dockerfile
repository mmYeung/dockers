FROM ubuntu:16.04

WORKDIR /app

ENV AGENT_VERSION=2.0.

## Download required Java
RUN apt-get update && apt-get install -y \
    openjdk-8-jre \
    unzip

COPY ./AGeNT_${AGENT_VERSION}.zip .

RUN unzip AGeNT_${AGENT_VERSION}.zip && \
    rm AGeNT_${AGENT_VERSION}.zip && \
    mv agent agent_${AGENT_VERSION} && \
    cd agent_${AGENT_VERSION}/lib && \
    mv Agent-*.jar Agent.jar && \
    mv junit-*.jar junit.jar && \
    mv locatit-*.jar locatit.jar && \
    mv trimmer-*.jar trimmer.jar

# ENV LIB=/app/agent_${AGENT_VERSION}/lib:$LIB

# ENV CLASSPATH=/app/agent_${AGENT_VERSION}/lib/Agent.jar:/app/agent_${AGENT_VERSION}/lib/junit.jar:/app/agent_${AGENT_VERSION}/lib/locatit.jar:/app/agent_${AGENT_VERSION}/lib/trimmer.jar:$CLASSPATH

WORKDIR /app/agent_${AGENT_VERSION}/lib

CMD [ "java -jar " ]