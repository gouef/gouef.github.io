<img align=right width="168" src="docs/gouef_logo.png">

# Standards

The `standards` package provides a set of interfaces and implementations for [caching](#caching) and [logging](#logging) functionalities, designed to be flexible and extensible. It includes interfaces for cache operations, a logger interface, and implementations for both cache and logging functionalities.

[![Static Badge](https://img.shields.io/badge/Github-gouef%2Fstandards-blue?style=for-the-badge&logo=github&link=github.com%2Fgouef%2Fstandards)](https://github.com/gouef/standards)

[![GoDoc](https://pkg.go.dev/badge/github.com/gouef/standards.svg)](https://pkg.go.dev/github.com/gouef/standards)
[![GitHub stars](https://img.shields.io/github/stars/gouef/standards?style=social)](https://github.com/gouef/standards/stargazers)
[![Go Report Card](https://goreportcard.com/badge/github.com/gouef/standards)](https://goreportcard.com/report/github.com/gouef/standards)
[![codecov](https://codecov.io/github/gouef/standards/branch/main/graph/badge.svg?token=YUG8EMH6Q8)](https://codecov.io/github/gouef/standards)

## Versions
![Stable Version](https://img.shields.io/github/v/release/gouef/standards?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/standards?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/standards?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)

## Installation

To install the `standards` package, use the following Go command:

```bash
go get -u github.com/gouef/standards
```

## Caching
The `standards` package includes different types of cache interfaces and implementations.

### Cache Interface

The `Cache` interface defines methods for working with cache items. It provides functionality for retrieving, saving, deleting, and clearing cache items.

#### Methods:
- `GetItem(key string) CacheItem`: Retrieves a cache item by key or nil if not exists.
- `GetItems(keys ...string) []CacheItem`: Retrieves multiple cache items by keys.
- `HasItem(key string) bool`: Checks if a cache item exists.
- `Clear() error`: Clears all items in the cache.
- `DeleteItem(key string) error`: Deletes a specific cache item.
- `DeleteItems(keys ...string) error`: Deletes multiple cache items.
- `Save(item CacheItem) error`: Immediately persists a cache item.
- `SaveDeferred(item CacheItem) error`: Marks a cache item to be saved later.
- `Commit() error`: Persists any deferred cache items.

### CacheItem Interface
The `CacheItem` interface represents individual cache items with methods for interacting with them.

#### Methods:
- `GetKey() string`: Returns the key of the cache item.
- `Get() any`: Retrieves the value of the cache item.
- `IsHit() bool`: Confirms if the cache lookup was a hit.
- `Set(value any) (CacheItem, error)`: Sets the value of the cache item.
- `ExpiresAt(expiration time.Time) (CacheItem, error)`: Sets the absolute expiration time for the cache item.
- `ExpiresAfter(t time.Duration)`: Sets the relative expiration time for the cache item.

### CacheSimple Interface
The `CacheSimple` interface provides simplified cache operations with key-value pairs.

#### Methods:
- `Get(key string, defaultValue any) any`: Retrieves a value from the cache.
- `GetMultiply(keys []string, defaultValue any) []any`: Retrieves multiple values from the cache.
- `Has(key string) bool`: Checks if a key exists in the cache.
- `Clear() error`: Clears all cache items.
- `Delete(key string) error`: Deletes a specific cache item.
- `DeleteMultiply(keys ...string) error`: Deletes multiple cache items.
- `Set(key string, item any) error`: Adds or updates a cache item.
- `SetMultiply(values []any, ttl time.Duration) error`: Adds or updates multiple cache items with a TTL.

## Logging
The `standards` package provides a logging system with multiple log levels, making it easy to implement custom loggers or use the provided default LoggerNull.

### Logger Interface
The `Logger` interface defines methods for logging at various levels.

#### Methods:
- `Emergency(message string, context []any) error`: Logs an emergency level message.
- `Alert(message string, context []any) error`: Logs an alert level message.
- `Critical(message string, context []any) error`: Logs a critical level message.
- `Error(message string, context []any) error`: Logs an error message.
- `Warning(message string, context []any) error`: Logs a warning message.
- `Notice(message string, context []any) error`: Logs a notice level message.
- `Info(message string, context []any) error`: Logs an info level message.
- `Debug(message string, context []any) error`: Logs a debug level message.
- `Log(level LogLevel, message string, context []any) error`: Logs a message with an arbitrary log level.

### LogLevel Enum
The `LogLevel` type defines the following log levels:

- `EMERGENCY`: System is unusable.
- `ALERT`: Immediate action required.
- `CRITICAL`: Critical conditions.
- `ERROR`: Errors that do not require immediate action.
- `WARNING`: Exceptional occurrences, not errors.
- `NOTICE`: Normal but significant events.
- `INFO`: Informative events.
- `DEBUG`: Detailed debug information.

### LoggerNull Implementation
The `LoggerNull` type implements the Logger interface and provides a no-op (no operation) logger. It does not perform any logging, making it useful for scenarios where logging is not required.

#### Example usage:

```go
package main

import (
	"github.com/gouef/standards"
	"fmt"
)

func main() {
	// Create a new LoggerNull instance
	logger := &standards.LoggerNull{}

	// Example of using the logger methods
	logger.Info("Informational message", nil)
	logger.Warning("Warning message", nil)
	logger.Error("Error message", nil)
}

```

### LoggerAware Interface
The `LoggerAware` interface provides a SetLogger method to inject a logger into an object that requires logging functionality.

#### Method:
- `SetLogger(logger Logger)`: Injects a logger instance into the object.

## Contributing

Read [Contributing](CONTRIBUTING.md)

## Contributors

<div>
<span>
  <a href="https://github.com/JanGalek"><img src="https://raw.githubusercontent.com/gouef/standards/refs/heads/contributors-svg/.github/contributors/JanGalek.svg" alt="JanGalek" /></a>
</span>
<span>
  <a href="https://github.com/actions-user"><img src="https://raw.githubusercontent.com/gouef/standards/refs/heads/contributors-svg/.github/contributors/actions-user.svg" alt="actions-user" /></a>
</span>
</div>

