FROM ubuntu:latest

COPY packages dependancies

ENV DEBIAN_FRONTEND noninteractive

# Install ubuntu base modules
RUN apt update && apt -y upgrade \ 
    && apt install -y $(cat dependancies) \
    && updatedb
    
RUN apt install -y python3 python3-dev python3-pip

# Clone git repo
RUN cd /tmp \
    && git clone https://github.com/ecatanzani/HEALPix-Docker.git

# Install cfitsio
RUN mkdir /usr/local/cfitsio \
    && cd /tmp/HEALPix-Docker/dependancies/dcfitsio \
    && tar -xzf cfitsio3450.tar.gz \
    && cd cfitsio \
    && ./configure --prefix=/usr/local/cfitsio \
    && make \
    && make install

# Install g77 libraries
RUN cd /tmp/HEALPix-Docker/dependancies/dg77 \
    && tar -xvf g77_pack_64bit.tar \
    &&  bash install.sh

# Creating HEALPix directory
RUN mkdir /HEALPix

# Install HEalPix
RUN cd /tmp/HEALPix-Docker/dependancies/dHEalPiX \
    && tar -xvzf Healpix_3.50_2018Dec10.tar.gz \
    && cp -r HEALPix/* /HEALPix \
    && cd /HEALPix \
    && make \
    && make test \
    && make clean \
    && make tidy \
    && make distclean

# Creating HEALPix volume
VOLUME /HEALPix
VOLUME /root
 
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
