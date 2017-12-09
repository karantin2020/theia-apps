FROM node:8-alpine
ARG THEIAVERSION=latest
ARG GOVERSION=1.9.2
ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go
RUN mkdir -p /go; \
    mkdir -p /lib64 && ln -sfb /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2; \
    apk add --no-cache ca-certificates; \
    apk add --no-cache --virtual=.build-dependencies curl git python; \
    curl -sS https://storage.googleapis.com/golang/go${GOVERSION}.linux-amd64.tar.gz | tar -C /usr/local -xzf - ; \
    go version; \
    go get -u -v github.com/ramya-rao-a/go-outline; \
    go get -u -v github.com/acroca/go-symbols; \
    go get -u -v github.com/nsf/gocode; \
    go get -u -v github.com/rogpeppe/godef; \
    go get -u -v golang.org/x/tools/cmd/godoc; \
    go get -u -v github.com/zmb3/gogetdoc; \
    go get -u -v github.com/golang/lint/golint; \
    go get -u -v github.com/fatih/gomodifytags; \
    go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs; \
    go get -u -v golang.org/x/tools/cmd/gorename; \
    go get -u -v sourcegraph.com/sqs/goreturns; \
    go get -u -v github.com/cweill/gotests/...; \
    go get -u -v golang.org/x/tools/cmd/guru; \
    go get -u -v github.com/josharian/impl; \
    go get -u -v github.com/haya14busa/goplay/cmd/goplay; \
    apk del --purge .build-dependencies; \
    rm -rf /go/src/*

WORKDIR /home/theia
ADD theia-go-docker/${THEIAVERSION}.package.json ./package.json

RUN yarn; \
    npx theia build
EXPOSE 3000
ENV SHELL /bin/ash
ENTRYPOINT [ "npx", "theia", "start", "/home/project", "--hostname=0.0.0.0" ]
