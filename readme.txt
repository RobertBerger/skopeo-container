$ skopeo copy docker://docker.io/nginx docker-archive:/tmp/nginx.tar
$ skopeo copy docker://docker.io/nginx oci-archive:/tmp/nginx.oci
$ skopeo copy docker://docker.io/nginx dir:/tmp/nginx-dir
$ skopeo copy docker://docker.io/nginx oci:/tmp/nginx-oci

skopeo copy docker://docker.io/reliableembeddedsystems/oci-lighttpd docker-archive:mala.tar

docker load -i mala.tar
Loaded image ID: sha256:458c2cb0b6385d0255ae556cd81b2418eda94bc037001a4e8252d961550d47d5


------

# --> for arm
skopeo copy docker://docker.io/reliableembeddedsystems/oci-lighttpd:latest-arm-v7 docker-archive:oci-lighttpd-latest-arm-v7.skopeo.tar:reliableembeddedsystems/oci-lighttpd


docker load -i oci-lighttpd-latest-arm-v7.skopeo.tar

docker pull reliableembeddedsystems/oci-lighttpd:latest
latest: Pulling from reliableembeddedsystems/oci-lighttpd
Digest: sha256:7f094c66d2d53b13891fb800d7103546b91887bdf034555df151966ddf4e75dc
Status: Image is up to date for reliableembeddedsystems/oci-lighttpd:latest
docker.io/reliableembeddedsystems/oci-lighttpd:latest

docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login
# <-- for arm


--------

# --> for arm without registry

#cd /workdir/build/container-arm-v7/tmp/deploy/images/container-arm-v7
#
#mkdir skopeo-experiments && cd skopeo-experiments
#
#skopeo copy oci:app-container-image-lighttpd-oci-container-arm-v7-20200718123036.rootfs-oci:latest docker-archive:oci-lighttpd-latest-arm-v7.skopeo.tar:reliableembeddedsystems/oci-lighttpd

on target:

scp student@192.168.42.1:/workdir/build/container-arm-v7/tmp/deploy/images/container-arm-v7/unzip/oci-lighttpd-latest-arm-v7.skopeo.tar .

docker load -i oci-lighttpd-latest-arm-v7.skopeo.tar

docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login

docker pull reliableembeddedsystems/oci-lighttpd:latest
latest: Pulling from reliableembeddedsystems/oci-lighttpd
09e7035ad22c: Already exists
Digest: sha256:7f094c66d2d53b13891fb800d7103546b91887bdf034555df151966ddf4e75dc
Status: Downloaded newer image for reliableembeddedsystems/oci-lighttpd:latest
docker.io/reliableembeddedsystems/oci-lighttpd:latest

++++ not sure what it pulled now +++++

docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login

# <-- for arm without registry

# --> rootfs tarball directly
Linux:

scp app-container-image-lighttpd-oci-container-arm-v7-20200723202138.rootfs.tar.bz2 root@192.168.42.123:/tmp

target:

cd /tmp




docker import app-container-image-lighttpd-oci-container-arm-v7-20200723202138.rootfs.tar.bz2 reliableembeddedsystems/oci-lighttpd:latest
sha256:9ab4f369326f298eac7e337abc53fa7f64053a3bdef2b6bd42559f7de48944c7
root@imx6q-phytec-mira-rdk-nand:/tmp# docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login
[312769.634145] docker0: port 1(veth1a167bc) entered blocking state
[312769.640286] docker0: port 1(veth1a167bc) entered disabled state
[312769.646583] device veth1a167bc entered promiscuous mode
[312771.911535] eth0: renamed from veth7229be4
[312771.961140] IPv6: ADDRCONF(NETDEV_CHANGE): veth1a167bc: link becomes ready
[312771.968284] docker0: port 1(veth1a167bc) entered blocking state
[312771.974349] docker0: port 1(veth1a167bc) entered forwarding state
root@4bdd6ed053b4:/# ps
  PID USER       VSZ STAT COMMAND
    1 root      2908 S    /bin/ash --login
    7 root      2908 R    ps
root@4bdd6ed053b4:/#
root@4bdd6ed053b4:/etc/lighttpd# /etc/lighttpd restart
/bin/ash: /etc/lighttpd: Permission denied
root@4bdd6ed053b4:/etc/lighttpd#

# <-- rootfs tarball directly

# --> skopeo nc

poky container:

cd /workdir/build/imx6q-phytec-mira-rdk-nand-virt-wic-mc/tmp-container-arm-v7-resy-container/deploy/images/container-arm-v7

rm -rf unzip

mkdir unzip && cd unzip

export IMAGE="app-container-image-lighttpd-oci-container-arm-v7"

tar xvf ../${IMAGE}*.tar

OCI="$(ls)" && echo ${OCI}

export CONTAINER="oci-lighttpd"
export TAG="latest-arm-v7"
export DOCKER_USER="reliableembeddedsystems"

skopeo copy oci:${OCI} docker-archive:${CONTAINER}-${TAG}.skopeo.tar.docker-archive:${DOCKER_USER}/${CONTAINER}

mv ${CONTAINER}-${TAG}.skopeo.tar.docker-archive ../

linux:

cd /workdir/build/imx6q-phytec-mira-rdk-nand-virt-wic-mc/tmp-container-arm-v7-resy-container/deploy/images/container-arm-v7

scp oci-lighttpd-latest-arm-v7.skopeo.tar.docker-archive root@192.168.42.123:/tmp

target:

cd /tmp

docker load -i oci-lighttpd-latest-arm-v7.skopeo.tar.docker-archive
ac290e1846c3: Loading layer [==================================================>]  6.676MB/6.676MB
Loaded image: reliableembeddedsystems/oci-lighttpd:latest

docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login

/etc/init.d/lighttpd restart


Hmmmmmmm

latest: Pulling from reliableembeddedsystems/oci-lighttpd
09e7035ad22c: Already exists
Digest: sha256:7f094c66d2d53b13891fb800d7103546b91887bdf034555df151966ddf4e75dc
Status: Downloaded newer image for reliableembeddedsystems/oci-lighttpd:latest
docker.io/reliableembeddedsystems/oci-lighttpd:latest

++++ not sure what it pulled now +++++

docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login

/etc/init.d/lighttpd restart


# <-- skopeo mc


# --> rootfs tarball directly mc @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Linux:

cd /workdir/build/imx6q-phytec-mira-rdk-nand-virt-wic-mc/tmp-container-arm-v7-resy-container/deploy/images/container-arm-v7

scp app-container-image-lighttpd-oci-container-arm-v7-20200724150524.rootfs.tar.bz2 root@192.168.42.123:/tmp

target:

cd /tmp

docker import app-container-image-lighttpd-oci-container-arm-v7-20200724150524.rootfs.tar.bz2 reliableembeddedsystems/oci-lighttpd:latest
sha256:40af155f7ca7910593c0e07e339a1dc96d4b84c94d156b77a48c59ffaf34f8ab

docker run -p 8079:80 --interactive --tty --entrypoint=/bin/ash reliableembeddedsystems/oci-lighttpd:latest --login

/etc/init.d/lighttpd restart

With web browser:

http://192.168.42.123:8079

docker pull reliableembeddedsystems/oci-lighttpd:latest

# <-- rootfs tarball directly mc @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
