## Alamode
    https://github.com/ttadano/alamode

## Docker installation (archlinux)
    pacman -S docker
    systemctl start docker
    systemctl enable docker

## alamode + docker

    docker pull alamode:1.0.2-ubuntu
    docker images

    cd alamode/example/Si
    docker run -it --rm -v $(pwd):/workplace alamode:1.0.2 alm /workplace/si_alm.in
    docker run -it --rm -v $(pwd):/workplace alamode:1.0.2 anphon /workplace/si_phband.in

    docker run -it --rm -v $(pwd):/workplace alamode:1.0.2 bash

## References
Based on https://github.com/wuhanstudio/alamode-docker (ubuntu version)
