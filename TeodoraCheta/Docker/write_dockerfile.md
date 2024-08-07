1. Layers

-> Each instruction in a Dockerfile roughly translates to an image layer
-> When you run a build, the builder attempts to reuse layers from earlier builds
-> layer unchanged -> builder picks it up from the build cache
-> layer changed -> must be rebuilt

-> download amd install dependencies before copying the source code
-> builder can reuse dependencies even when changes occur on the source code

 # syntax=docker/dockerfile:1
  FROM golang:1.21-alpine
  WORKDIR /src
- COPY . .
+ COPY go.mod go.sum .
  RUN go mod download
+ COPY . .
  RUN go build -o /bin/client ./cmd/client
  RUN go build -o /bin/server ./cmd/server
  ENTRYPOINT [ "/bin/server" ]

2. Multi-stage

-> build stage represented by a FROM instruction
-> allow to create a final image with a smaller footprint, containing only what's needed to run your program

# syntax=docker/dockerfile:1
  FROM golang:1.21-alpine
  WORKDIR /src
  COPY go.mod go.sum .
  RUN go mod download
  COPY . .
  RUN go build -o /bin/client ./cmd/client
  RUN go build -o /bin/server ./cmd/server
+
+ FROM scratch
+ COPY --from=0 /bin/client /bin/server /bin/
  ENTRYPOINT [ "/bin/server" ]

-> allow you to run build steps in parallel, making your build pipeline faster and more efficient

# syntax=docker/dockerfile:1
FROM golang:1.21-alpine AS base
WORKDIR /src
COPY go.mod go.sum /src/
RUN go mod download
COPY . .

# build client
FROM base AS build-client
RUN go build -o /bin/client ./cmd/client

# build server
FROM base AS build-server
RUN go build -o /bin/server ./cmd/server

# copy client binary to client image
FROM scratch AS client
COPY --from=build-client /bin/client /bin/
ENTRYPOINT [ "/bin/client" ]

# copy server binary to server image
FROM scratch AS server
COPY --from=build-server /bin/server /bin/
ENTRYPOINT [ "/bin/server" ]

Build the client image:


docker build -t run-client --target=client .


Build the server image:


docker build -t run-server --target=server .

3. BUild arguments

# syntax=docker/dockerfile:1

# defining variable
ARG GO_VERSION=1.21

# using variable
FROM golang:${GO_VERSION}-alpine AS base
WORKDIR /src
COPY go.mod go.sum /src/
RUN go mod download
COPY . .

FROM base AS build-client
RUN go build -o /bin/client ./cmd/client

FROM base AS build-server
RUN go build -o /bin/server ./cmd/server

FROM scratch AS client
COPY --from=build-client /bin/client /bin/
ENTRYPOINT [ "/bin/client" ]

FROM scratch AS server
COPY --from=build-server /bin/server /bin/
ENTRYPOINT [ "/bin/server" ]

Build the image:


docker build --build-arg="GO_VERSION=1.22" .

4. Export binaries

Add next line to the /root/app/Dockerfile :


# syntax=docker/dockerfile:1
ARG GO_VERSION=1.21
FROM golang:${GO_VERSION}-alpine AS base
WORKDIR /src
COPY go.mod go.sum /src/
RUN go mod download
COPY . .

FROM base AS build-client
RUN go build -o /bin/client ./cmd/client

FROM base AS build-server
RUN go build -o /bin/server ./cmd/server

FROM scratch AS client
COPY --from=build-client /bin/client /bin/
ENTRYPOINT [ "/bin/client" ]

FROM scratch AS server
COPY --from=build-server /bin/server /bin/
ENTRYPOINT [ "/bin/server" ]

# exporting binaries from server and client images
FROM scratch AS binaries
COPY --from=server /bin/server /
COPY --from=client /bin/client /

Export binaries:


docker build --output=/root/app --target=binaries .

