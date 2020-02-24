FROM alpine:3.9

RUN apk add --no-cache curl
COPY ./build/VERSION VERSION
RUN version=$(cat VERSION) && curl -L "https://github.com/kubernetes/kompose/releases/download/v${version}/kompose-linux-amd64" -o kompose

FROM golang:alpine

RUN apk add git make &&\
    mkdir -p $GOPATH/src/github.com/kubernetes &&\
    git clone https://github.com/kubernetes/kompose.git $GOPATH/src/github.com/kubernetes/kompose &&\
    cd $GOPATH/src/github.com/kubernetes/kompose &&\
    go build -o kompose main.go &&\
    mv $GOPATH/src/github.com/kubernetes/kompose/kompose /kompose

FROM alpine:3.9

COPY --from=1 /kompose /usr/bin/kompose
RUN chmod +x /usr/bin/kompose
