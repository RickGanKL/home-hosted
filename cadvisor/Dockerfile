# Builder
FROM arm64v8/golang as builder

ARG VERSION=${VERSION}
# ENV VERSION "${VERSION}"

RUN apt-get update && apt-get install -y git dmsetup && apt-get clean

RUN git clone --branch ${VERSION} https://github.com/google/cadvisor.git /go/src/github.com/google/cadvisor

WORKDIR /go/src/github.com/google/cadvisor

RUN make build

# Image for usage
FROM arm64v8/debian

COPY --from=builder /go/src/github.com/google/cadvisor/cadvisor /usr/bin/cadvisor

EXPOSE 8080
ENTRYPOINT ["/usr/bin/cadvisor", "-logtostderr"]
