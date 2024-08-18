FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Update and install necessary packages
RUN apt-get update && apt-get install -y \
    unzip \
    graphviz \
    curl \
    musescore3 \
    python3-pip \
    python3-dev \
    build-essential \
    libhdf5-dev \
    libhdf5-serial-dev \
    hdf5-tools \
    pkg-config \
    cmake \
    git \
    python3-h5py \
    && apt-get clean

# Upgrade pip
RUN pip install --upgrade pip

WORKDIR /app

# fix typeDict error
RUN pip install numpy --upgrade

# Install h5py without using --no-binary
RUN pip install h5py

# Copy the requirements file and install the rest of the Python dependencies
COPY ./requirements.txt /app
RUN pip install -r /app/requirements.txt

# Hack to get around tensorflow-io issue - https://github.com/tensorflow/io/issues/1755
RUN pip install tensorflow-io
RUN pip uninstall -y tensorflow-io

COPY /notebooks/. /app/notebooks
COPY /scripts/. /app/scripts

ENV PYTHONPATH="${PYTHONPATH}:/app"
