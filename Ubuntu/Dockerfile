FROM ubuntu:latest

# Install ubuntu base modules
RUN apt-get update \
    && apt install -y apt-utils build-essential gfortran wget locate 

RUN apt install -y python3 python3-dev python3-pip

# Install cfitsio
RUN cd /tmp \
    && wget https://mega.nz/#!XMlQyQQa \
    && tar -xzf cfitsio3450.tar.gz \
    && cd cfitsio \
    && ./configure --prefix=/usr/local \
    && make \
    && make install

# Install HEalPix
RUN cd /tmp \
    && wget https://mega.nz/#!zI02UCYK

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*