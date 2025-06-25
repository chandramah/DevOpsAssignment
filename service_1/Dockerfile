FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go mod download
RUN go build -o main .

FROM alpine:latest
WORKDIR /app
RUN apk add --no-cache curl  # Add curl for health checks
COPY --from=builder /app/main .
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:8001/ping || exit 1
EXPOSE 8001
CMD ["./main"]