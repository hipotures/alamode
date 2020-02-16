## References
Based on https://github.com/wuhanstudio/alamode-docker (ubuntu version)

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
docker run -it --rm -v $(pwd):/tmp alamode:1.0.2 alm /tmp/si_alm.in
