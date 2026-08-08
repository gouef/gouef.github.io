<img align=right width="168" src="docs/gouef_logo.png">

# health

<p align="center">
  <strong>lightweight health checks for Go services</strong><br/>
  Register custom checks, verify HTTP endpoints and database connectivity, monitor disk usage, and expose a Gin health endpoint.
</p>

<p align="center">
  <a href="#-features"><strong>Features</strong></a>
  ·
  <a href="#-quick-start"><strong>Quick start</strong></a>
  ·
  <a href="#-testing"><strong>Testing</strong></a>
  ·
  <a href="#-contributing"><strong>Contributing</strong></a>
</p>

[![Static Badge](https://img.shields.io/badge/Github-gouef%2Fhealth-blue?style=for-the-badge&logo=github&link=github.com%2Fgouef%2Fhealth)](https://github.com/gouef/health)
[![GoDoc](https://pkg.go.dev/badge/github.com/gouef/health.svg)](https://pkg.go.dev/github.com/gouef/health)
[![Go Report Card](https://goreportcard.com/badge/github.com/gouef/health)](https://goreportcard.com/report/github.com/gouef/health)
[![codecov](https://codecov.io/github/gouef/health/branch/main/graph/badge.svg?token=YUG8EMH6Q8)](https://codecov.io/github/gouef/health)

## ✨ Features

- Register custom checks with the Checker interface or FuncChecker
- Verify HTTP endpoints with HTTPChecker
- Check database availability with DBChecker
- Monitor free disk space with DiskChecker
- Expose results through a Gin-compatible handler

## 🚀 Quick start

Install the package in your project:

```bash
go get github.com/gouef/health
```

Example usage:

```go
package main

import (
    "context"
    "database/sql"
    "net/http"
    "time"

    _ "github.com/go-sql-driver/mysql"
    "github.com/gouef/health"
)

func main() {
    h := health.New(3 * time.Second)

    h.Register(health.NewFuncChecker("app", func(ctx context.Context) health.Result {
        return health.Result{Status: health.StatusUp, Type: "custom"}
    }))

    h.Register(health.NewHTTPChecker("api", "https://example.com", &http.Client{}))

    db, err := sql.Open("mysql", "user:pass@tcp(localhost:3306)/dbname")
    if err == nil {
        h.Register(health.NewDBChecker("database", db))
    }

    h.Register(health.NewDiskChecker("disk", "/", 100*1024*1024))
}
```

Expose it through Gin:

```go
import "github.com/gin-gonic/gin"

func main() {
    r := gin.New()
    r.GET("/health", h.Handler())
    _ = r.Run(":8080")
}
```

Example handler response:

```json
{
  "status": "UP",
  "services": {
    "app": {"status": "UP", "type": "custom", "response_time_ms": 0},
    "api": {"status": "UP", "type": "http", "response_time_ms": 42}
  }
}
```

## 🧪 Testing

Run the test suite:

```bash
go test ./...
```

Generate a coverage report:

```bash
go test -covermode=set -coverpkg=./... -coverprofile=coverage.txt . && go tool cover -func=coverage.txt
```

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development guidelines and contribution steps.

## Contributors

<div>
  <a href="https://github.com/gouef/health/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=gouef/health" />
  </a>
</div>
