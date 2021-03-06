FROM ubuntu:focal
MAINTAINER hipotures

# ---------------------------------------------------------------
# Prerequisites
# ---------------------------------------------------------------

RUN apt-get update
RUN apt-get install -y wget tar build-essential git vim libblas-dev liblapack-dev liblapacke-dev libboost-all-dev libfftw3-dev libeigen3-dev gfortran libsymspg1 libsymspg-dev
RUN rm -rf /var/lib/apt/lists/*
RUN cp /usr/include/eigen3/* /usr/include/ -r

# ---------------------------------------------------------------
# MPICH2
# ---------------------------------------------------------------

RUN mkdir -p /opt/mpich2
WORKDIR /opt/mpich2
RUN wget http://www.mpich.org/static/downloads/3.2.1/mpich-3.2.1.tar.gz
RUN tar -xvf mpich-3.2.1.tar.gz
WORKDIR /opt/mpich2/mpich-3.2.1
RUN ./configure --disable-fortran
RUN make && make install

# ---------------------------------------------------------------
# LAPACK
# ---------------------------------------------------------------

RUN mkdir -p /opt/lapack
WORKDIR /opt/lapack
RUN wget http://www.netlib.org/lapack/lapack-3.8.0.tar.gz
RUN tar -xvf lapack-3.8.0.tar.gz
WORKDIR /opt/lapack/lapack-3.8.0
RUN cp make.inc.example make.inc
RUN make blaslib lapacklib lapackelib
RUN cp librefblas.a /usr/lib/

# ---------------------------------------------------------------
# Boost
# ---------------------------------------------------------------

#apt-get install libboost-all-dev

# ---------------------------------------------------------------
# FFTW3
# ---------------------------------------------------------------

#apt-get install libfftw3-dev

# ---------------------------------------------------------------
# Eigen3
# ---------------------------------------------------------------

# apt-get install libeigen3-dev 

# ---------------------------------------------------------------
# ALAMODE
# ---------------------------------------------------------------

RUN wget https://github.com/ttadano/alamode/archive/v.1.0.2.tar.gz && \
    tar xvfz v.1.0.2.tar.gz && \
    rm v.1.0.2.tar.gz && \
    mv alamode-v.1.0.2 /opt/alamode


# TOOLS
WORKDIR /opt/alamode/tools
COPY Makefile.TOOLS Makefile
RUN make

# ANPHON
WORKDIR /opt/alamode/anphon
COPY Makefile.ANPHON Makefile
RUN make

# ALM
WORKDIR /opt/alamode/alm
COPY Makefile.ALM Makefile
RUN make

RUN mkdir /opt/work_dir
ENV PATH=$PATH:/opt/alamode/alm:/opt/alamode/anphon:/opt/alamode/tools
