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
