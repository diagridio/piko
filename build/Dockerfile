FROM golang:1.26.11 AS build

ARG version

WORKDIR /app

COPY . .

RUN CGO_ENABLED=0 go build -ldflags="-X github.com/andydunstall/piko/pkg/build.Version=$version" -o ./piko main.go


FROM alpine:latest

# The base image is only as new as its last publish, so take the package
# fixes Alpine has shipped since (OpenSSL, musl, zlib).
RUN apk upgrade --no-cache

COPY --from=build app/piko /bin/piko

ENTRYPOINT [ "/bin/piko" ]
