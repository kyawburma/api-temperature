FROM golang AS builder

ENV GO111MODULE=on

# Set the Current Working Directory inside the container
WORKDIR /app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .


WORKDIR /app/cmd/api-temperature

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GO111MODULE=on go build

FROM alpine

RUN apk add ca-certificates

COPY --from=builder /app/cmd/api-temperature/api-temperature /app/

ENTRYPOINT ["/app/api-temperature"]
