FROM {{ cookiecutter.image }}

WORKDIR /go/src/client
COPY client.go .

# Nexus: https://github.com/gammazero/nexus
RUN    go get github.com/gammazero/nexus/client \
    && go get github.com/gammazero/nexus/wamp \
    && go get github.com/gammazero/nexus/transport

RUN go build -ldflags "-linkmode external -extldflags -static" -a client.go

FROM scratch
COPY --from=0 /go/src/client/client /client
CMD ["/client", "ws://127.0.0.1:8080/ws", "realm1"]
