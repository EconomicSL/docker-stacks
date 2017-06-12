# Pull base image
FROM  ibillett/esl-base-docker:v0.1

RUN apt-get update -y && \
    apt-get install -y bzip2 wget && \
    apt-get clean

ENV HOME /root/
ENV SHELL /bin/bash
WORKDIR $HOME

RUN echo "Downloading Miniconda..." && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    $SHELL Miniconda3-latest-Linux-x86_64.sh -b && \
    rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH $HOME/miniconda3/bin:$PATH

COPY environment.yml $HOME

# Install various Python dependencies...
RUN conda env create -f environment.yml
