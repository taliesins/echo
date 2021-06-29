FROM golang:1.16.5-alpine as builder
WORKDIR /app/
COPY . .
RUN go build -o echoserver /app/main.go
RUN apk add openssl
RUN openssl genrsa -out server.key 2048 && openssl req -new -x509 -sha256 -key server.key -out server.crt -days 3650 -subj "/C=CA/ST=QC/O=Company, Inc./CN=echo.localhost" -addext "subjectAltName=DNS:echo.localhost,DNS:echo1.localhost,DNS:echo2.localhost"

FROM alpine:latest
WORKDIR /app/
COPY --from=builder /app/echoserver /app/echoserver
COPY --from=builder /app/server.key /app/server.key
COPY --from=builder /app/server.crt /app/server.crt
EXPOSE 5980
CMD ./echoserver -ssl