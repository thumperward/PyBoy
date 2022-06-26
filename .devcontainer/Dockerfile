FROM mcr.microsoft.com/vscode/devcontainers/base:debian

# Install additional OS packages.
ARG DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y --no-install-recommends \
  build-essential \
  python3-pip \
  npm \
  2>&1 && \
  rm -rf /var/lib/apt/lists/* 

# Install Python packages needed by the container (not package dependencies).
RUN pip3 install \
  poetry \
  pre-commit \
  detect-secrets \
  2>&1

# Install global node packages.
RUN npm install -g \
  markdownlint-cli \
  2>&1

# Install packages needed to build rgbasm (for boot rom).
# RUN apt install -y \
#   libsdl2-dev \
#   python3-pip \
#   python3-dev \
#   libtiff5-dev \
#   libjpeg62-turbo-dev \
#   libpng-dev \
#   zlib1g-dev \
#   pkg-config \
#   bison 

# Install rgbasm.
# RUN git clone git@github.com:gbdev/rgbds.git && \
#   cd rgbds && \
#   make && \
#   make install

# ARG pypy_version=pypy3.6-v7.3.0-linux64
# RUN curl -OL "https://bitbucket.org/pypy/pypy/downloads/$pypy_version.tar.bz2" && tar -xvf "$pypy_version.tar.bz2"
# ENV PATH="/$pypy_version/bin:${PATH}"

# WORKDIR /pyboy

# Work on Mac:
# $ /usr/X11/bin/xhost + 127.0.0.1
# $ docker run -v "$(pwd):/pyboy/" -v "$(pwd)/ROMs:/pyboy/ROMs" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=host.docker.internal:0 -e XDG_RUNTIME_DIR=/tmp -it baekalfen/pyboy:dev-latest bash

# Work on Ubuntu:
# $ /usr/X11/bin/xhost + 127.0.0.1
# $ docker run -v "$(pwd):/pyboy/" -v "$(pwd)/ROMs:/pyboy/ROMs" -v /tmp/.X11-unix:/tmp/.X11-unix:rw --device=/dev/dri -e DISPLAY -e XDG_RUNTIME_DIR=/tmp -it baekalfen/pyboy:dev-latest bash

# Inside the Docker container:
# Run the cythonized version in CPython:
# $ make clean && make && python3 -m pyboy ROMs/gamerom.gb # ROM path and any other arguments
# Run the PyPy version:
# $ pypy3 -m pyboy ROMs/gamerom.gb # ROM path and any other arguments
