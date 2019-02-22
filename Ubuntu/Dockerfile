FROM ubuntu:latest

COPY packages dependancies

# Install ubuntu base modules
RUN apt update && apt -y upgrade \ 
    && apt install -y $(cat dependancies) \
    && updatedb

RUN apt install -y python3 python3-dev python3-pip

# Clone git repo
RUN cd /tmp \
    && git clone https://github.com/ecatanzani/HEALPix-Docker.git

# Install cfitsio
RUN cd /tmp/HEALPix-Docker/dependancies/dcfitsio \
    && tar -xzf cfitsio3450.tar.gz \
    && cd cfitsio \
    && ./configure --prefix=/usr/local \
    && make \
    && make install

# Install HEalPix
RUN cd /tmp/HEALPix-Docker/dependancies/dHEalPiX
    
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*