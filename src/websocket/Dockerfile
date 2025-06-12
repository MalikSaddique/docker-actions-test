FROM golang:latest AS builder

WORKDIR /app
COPY . .
RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -o websocket ./src/websocket

FROM alpine:latest  
RUN apk --no-cache add ca-certificates

WORKDIR /root/
COPY --from=builder /app/src/websocket/.env.yaml .
COPY --from=builder /app/websocket .

CMD ["./websocket"]