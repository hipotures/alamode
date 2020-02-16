FROM archlinux:20200205
MAINTAINER hipotures

RUN pacman --noconfirm --needed -Syu \
    pacman-contrib \
    sudo \
    git \
    base-devel \
    go

# setup user aur
RUN useradd -m -g users -G wheel -s /bin/bash aur \
    && passwd -d aur \
    && echo 'aur ALL=(ALL) ALL' > /etc/sudoers.d/aur \
    && echo 'Defaults env_keep += "EDITOR"' >> /etc/sudoers.d/aur \
    && echo 'Set disable_coredump false' >> /etc/sudo.conf

# install aur
USER aur
RUN cd && \
    git clone https://aur.archlinux.org/yay.git && \
    cd yay && \
    makepkg -si --noconfirm

RUN yay -S --noconfirm --needed aur/mpich
RUN yay -S --noconfirm --needed extra/lapack
RUN yay -S --noconfirm --needed extra/boost-libs extra/fftw extra/eigen

# install alamode
USER root
RUN pacman --noconfirm --needed -S wget
RUN cd /opt && \
    wget https://github.com/ttadano/alamode/archive/v.1.1.0.tar.gz && \
    tar xvfz v.1.1.0.tar.gz && \
    mv alamode-v.1.1.0 alamode

WORKDIR /opt/alamode/tools
COPY Makefile.TOOLS Makefile
RUN make
