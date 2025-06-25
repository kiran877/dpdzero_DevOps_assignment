FROM golang:1.22-alpine AS builder

# Install curl for health checks
RUN apk add --no-cache curl

WORKDIR /app

# Copy source code
COPY main.go .

# Initialize Go module (even without external dependencies)
RUN go mod init myapp

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM alpine:latest

# Install curl for health checks
RUN apk --no-cache add curl

WORKDIR /root/

# Copy the binary from builder stage
COPY --from=builder /app/main .

EXPOSE 8001

CMD ["./main"]