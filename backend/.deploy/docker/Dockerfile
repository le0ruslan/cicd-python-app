FROM golang:1.20 AS builder

WORKDIR /app

COPY go.* .

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 go build -o backend-app ./cmd/main.go

FROM alpine:3.14

WORKDIR /app

RUN addgroup -S appuser && adduser -S appuser -G appuser

RUN apk update && apk add --no-cache \
    curl=8.0.1-r0 \
    && rm -rf /var/cache/apk/*

COPY --from=builder /app/backend-app /app/backend-app

COPY --from=builder /app/packages/db/migrations /packages/db/migrations

USER appuser

EXPOSE 8081

CMD ["./backend-app"]
