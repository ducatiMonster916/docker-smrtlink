FROM ubuntu:18.04
LABEL Author="Roberto Lleras (rolleras@microsoft.com)"

# System configuration
RUN chmod a+w /opt

# Install delendencies
RUN apt-get update && apt-get install -y \
    curl \
    default-jre \
    locales \
    net-tools \
    unzip \
    rsync \
    libc6

# Satisfy SMRT Link Server Environment Assumptions

## "ensure that the host system locale is set to LANG=en_US.UTF-8"
RUN locale-gen "en_US.UTF-8"
RUN update-locale LANG=en_US.UTF-8


# Download and install SMRT Link v9.0.0 per instructions at http://www.pacb.com/support/software-downloads/
ADD https://downloads.pacbcloud.com/public/software/installers/smrtlink_9.0.0.92188.zip smrtlink_9.0.0.92188.zip
RUN unzip -P nX4dmaR% smrtlink_9.0.0.92188.zip

ENV SMRT_USER=smrtanalysis
RUN useradd -ms /bin/bash $SMRT_USER
USER $SMRT_USER


ENV SMRT_ROOT=/opt/pacbio/smrtlink
RUN ./smrtlink_9.0.0.92188.run --rootdir $SMRT_ROOT --batch --ignore-system-check --smrttools-only
