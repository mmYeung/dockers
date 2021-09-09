FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build

WORKDIR /app

ENV PISCES_VERSION=5.3.0.0

RUN wget https://github.com/tamsen/Pisces/archive/refs/tags/v${PISCES_VERSION}.tar.gz

RUN tar -xzvf v${PISCES_VERSION}.tar.gz

RUN cd Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION} && tar -xzf Pisces_${PISCES_VERSION}.tar.gz && tar -xzf Hygea_${PISCES_VERSION}.tar.gz && tar -xzf Stitcher_${PISCES_VERSION}.tar.gz && tar -xzf GeminiMulti_${PISCES_VERSION}.tar.gz && tar -xzf Gemini_${PISCES_VERSION}.tar.gz && tar -xzf VariantQualityRecalibration_${PISCES_VERSION}.tar.gz

RUN mkdir /app/Pisces_v${PISCES_VERSION}

RUN mv Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION}/Pisces_${PISCES_VERSION}/* /app/Pisces_v${PISCES_VERSION}

RUN mv Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION}/Hygea_${PISCES_VERSION}/* /app/Pisces_v${PISCES_VERSION}

RUN mv Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION}/Stitcher_${PISCES_VERSION}/* /app/Pisces_v${PISCES_VERSION}

RUN mv Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION}/GeminiMulti_${PISCES_VERSION}/* /app/Pisces_v${PISCES_VERSION}

RUN mv Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION}/Gemini_${PISCES_VERSION}/* /app/Pisces_v${PISCES_VERSION}

RUN mv Pisces-${PISCES_VERSION}/binaries/${PISCES_VERSION}/VariantQualityRecalibration_${PISCES_VERSION}/* /app/Pisces_v${PISCES_VERSION}

RUN rm -r Pisces-${PISCES_VERSION} && rm v${PISCES_VERSION}.tar.gz

WORKDIR /app/Pisces_v${PISCES_VERSION}

ENTRYPOINT [ "dotnet" ]