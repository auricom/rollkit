# Make sure to build this from the root of the directory: rollkit
# docker build -f apps/evm/single/Dockerfile -t ghcr.io/rollkit/rollkit-evm-single:<version> .

FROM golang:1.24-alpine AS build-env

WORKDIR /src

COPY . .

# Uncomment the following lines to build the binary from source in the dockerfile directly
# WORKDIR /src/apps/evm/single

# RUN go mod tidy -compat=1.19 && \
#     CGO_ENABLED=0 go build -o /src/evm-single .


FROM alpine:3.18.3

WORKDIR /root

# Copy the binary from evm-single
# Make sure to build it first with the following command:
# GOOS=linux GOARCH=amd64 go build -o evm-single .
COPY apps/evm/single/evm-single /usr/bin/evm-single

# Uncomment the following lines to build the binary from source in the dockerfile directly
# COPY --from=build-env /src/evm-single /usr/bin/evm-single
COPY apps/evm/single/entrypoint.sh /usr/bin/entrypoint.sh
RUN chmod +x /usr/bin/entrypoint.sh

ENTRYPOINT ["/usr/bin/entrypoint.sh"]
