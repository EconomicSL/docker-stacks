# Pull base image
FROM  ibillett/esl-base-docker:v0.1

RUN apt-get update -y && \
    apt-get install -y bzip2 wget && \
    apt-get clean

ENV CONDA_DIR /opt/conda
ENV NB_USER esl
ENV NB_UID 1000
ENV HOME /root/
ENV SHELL /bin/bash
WORKDIR $HOME

# Create esl user with UID=1000 and in the 'users' group
RUN useradd -m -s /bin/bash -N -u 1000 esl && \
    mkdir -p $CONDA_DIR && \
    chown $NB_USER $CONDA_DIR

RUN cd /tmp && \
    mkdir -p $CONDA_DIR && \
    echo "Downloading Miniconda..." && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    $SHELL Miniconda3-latest-Linux-x86_64.sh -b && \
    rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH /root/miniconda3/bin:$PATH

COPY environment.yml $HOME

# Install various Python dependencies...
RUN conda env create -f environment.yml

EXPOSE 8888

ENTRYPOINT ["/bin/bash", "-c"]

# Give the esl user full access on the /root/ folder
RUN chown $NB_USER $HOME
# Switch to esl user for security reasons
USER $NB_USER

#Activate our python environment and start the jupyter notebook
CMD ["source activate base-python && jupyter notebook --ip=0.0.0.0"]
