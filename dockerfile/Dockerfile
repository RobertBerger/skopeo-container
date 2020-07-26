FROM golang:1.14-alpine AS builder

RUN apk add --no-cache \
    git \
    make \
    gcc \
    musl-dev \
    btrfs-progs-dev \
    lvm2-dev \
    gpgme-dev \
    glib-dev || apk update && apk upgrade

WORKDIR /go/src/github.com/containers/skopeo
RUN git clone https://github.com/containers/skopeo.git .
RUN git checkout v1.1.0 && git checkout -b v1.1.0
# This seems to work with docker hub:
# skopeo version 0.1.41-dev commit: e955849f0aca02eb8a179808f0952e8cbea43ed7
#RUN git checkout e955849f0aca02eb8a179808f0952e8cbea43ed7
#RUN git checkout -b 0.1.41-dev
RUN make binary-local-static DISABLE_CGO=1
RUN /go/src/github.com/containers/skopeo/skopeo --version

FROM alpine:3.12
run apk add --no-cache ca-certificates jq curl
COPY --from=builder /go/src/github.com/containers/skopeo/skopeo /usr/local/bin/skopeo
COPY --from=builder /go/src/github.com/containers/skopeo/default-policy.json /etc/containers/policy.json
#ENTRYPOINT ["/usr/local/bin/skopeo"]
#CMD ["--help"]
