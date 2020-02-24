FROM golang:alpine

RUN apk add git make &&\
    mkdir -p $GOPATH/src/github.com/kubernetes &&\
    git clone https://github.com/kubernetes/kompose.git $GOPATH/src/github.com/kubernetes/kompose &&\
    cd $GOPATH/src/github.com/kubernetes/kompose &&\
    go build -o kompose main.go &&\
    mv $GOPATH/src/github.com/kubernetes/kompose/kompose /kompose

FROM alpine:3.9

COPY --from=0 /kompose /usr/bin/kompose
RUN chmod +x /usr/bin/kompose
