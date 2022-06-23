ARG HUB=docker.io
FROM ${HUB}/library/golang:alpine AS build

ARG VERSION
ENV VERSION=${VERSION}

WORKDIR /app

COPY scripts/ ./scripts/
COPY vendor/ ./vendor/
COPY go.mod ./
COPY go.sum ./
COPY *.go ./

RUN apk add --no-cache bash git

RUN bash scripts/build

FROM alpine

COPY --from=build /app/bin/local-path-provisioner /usr/bin/
CMD ["local-path-provisioner"]
