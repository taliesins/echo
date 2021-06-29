FROM golang:1.16.5-alpine as builder
WORKDIR /app/
COPY . .
RUN go build -o echoclient /app/main.go

FROM alpine:latest
WORKDIR /app/
COPY --from=builder /app/echoclient /app/echoclient
EXPOSE 5980
CMD ./echoclient -ssl