---
layout: minimal
title: Golang Code Quality
nav_enabled: true
parent: Open Source Projects
nav_order: 7
---
# Golang Standards & Style Guide

## Philosophy

Go is opinionated by design. The toolchain enforces most formatting automatically — your job is to work *with* the language, not fight it. Where Python rewards flexibility, Go rewards clarity and explicitness. Adopt Go idioms rather than porting Python habits.

---

## Toolchain (Non-Negotiable)

These tools are mandatory, not optional. Run them before every commit.

| Tool | Purpose | Command |
|------|---------|---------|
| `gofmt` | Canonical formatting | `gofmt -w .` |
| `goimports` | Format + manage imports | `goimports -w .` |
| `go vet` | Catches common bugs | `go vet ./...` |
| `staticcheck` | Advanced static analysis | `staticcheck ./...` |
| `golangci-lint` | Aggregated linting | `golangci-lint run` |

Configure pre-commit hooks so formatting is never a manual step.

```toml
# .golangci.yml
linters:
  enable-all: true
  disable:
    - exhaustivestruct   # Too noisy for general use
    - gochecknoglobals   # Sometimes necessary

linters-settings:
  govet:
    enable-all: true
  cyclop:
    max-complexity: 10
```

---

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Variables | `camelCase` | `userCount`, `totalItems` |
| Constants | `camelCase` or `PascalCase` | `maxRetries`, `DefaultTimeout` |
| Functions / Methods | `camelCase` (unexported), `PascalCase` (exported) | `parseToken()`, `FetchUser()` |
| Types / Structs | `PascalCase` | `UserRepository`, `ParsedResult` |
| Interfaces | `PascalCase`, single-method = verb + `er` | `Reader`, `Stringer`, `UserFetcher` |
| Packages | lowercase, single word | `auth`, `httputil`, `store` |
| Error variables | `ErrXxx` for sentinel errors | `ErrNotFound`, `ErrTimeout` |
| Test files | `_test.go` suffix | `user_test.go` |

**Key difference from Python:** exported (public) identifiers start with a capital letter. Unexported identifiers start lowercase. This is enforced by the compiler, not convention.

```go
// Unexported — only accessible within the package
type userCache struct {
    entries map[string]User
}

func (c *userCache) get(id string) (User, bool) {
    u, ok := c.entries[id]
    return u, ok
}

// Exported — accessible from other packages
type UserRepository struct {
    cache *userCache
}

func (r *UserRepository) FindByID(id string) (User, error) {
    // ...
}
```

---

## Error Handling

Go has no exceptions. Errors are values returned explicitly. Treat them as first-class citizens.

### Core Rules

- **Always handle errors.** Never assign to `_` unless you have an explicit, commented reason.
- **Wrap errors with context** using `fmt.Errorf("operation failed: %w", err)`.
- **Sentinel errors** for known, checkable conditions; custom types for structured errors.
- Check errors immediately after the call — don't defer checking.

```go
// Bad — ignored error
file, _ := os.Open(path)

// Bad — error checked too late
result, err := doThing()
doOtherThing()  // runs even if doThing failed
if err != nil {
    return err
}

// Good — immediate check, wrapped context
result, err := fetchUser(ctx, id)
if err != nil {
    return fmt.Errorf("get user profile: %w", err)
}
```

### Custom Error Types

Use custom errors when callers need to inspect the error beyond its message.

```go
// Sentinel — for simple, known conditions
var (
    ErrNotFound   = errors.New("not found")
    ErrUnauthorized = errors.New("unauthorized")
)

// Structured — when callers need fields
type ValidationError struct {
    Field   string
    Message string
}

func (e *ValidationError) Error() string {
    return fmt.Sprintf("validation failed on %s: %s", e.Field, e.Message)
}

// Checking error types
if errors.Is(err, ErrNotFound) {
    // handle not found
}

var valErr *ValidationError
if errors.As(err, &valErr) {
    log.Printf("bad field: %s", valErr.Field)
}
```

---

## Types & Interfaces

### Interfaces

Go interfaces are **implicit** — a type satisfies an interface simply by implementing its methods. This is structural typing without declaration.

```go
// Define small, focused interfaces
type Storer interface {
    Store(ctx context.Context, key string, value []byte) error
}

type Fetcher interface {
    Fetch(ctx context.Context, key string) ([]byte, error)
}

// Compose interfaces when needed
type StoreFetcher interface {
    Storer
    Fetcher
}

// Accept interfaces, return concrete types
// (the "accept interfaces, return structs" principle)
func NewProcessor(store Storer) *Processor {
    return &Processor{store: store}
}
```

### Structs

Use structs for structured data. Prefer explicit field names in literals.

```go
// Bad — positional, fragile
user := User{"alice", "alice@example.com", 30}

// Good — explicit fields
user := User{
    Name:  "alice",
    Email: "alice@example.com",
    Age:   30,
}
```

### Zero Values

Design structs so the zero value is useful or safe. Document when it isn't.

```go
// Good — zero value is a valid, empty buffer
type Buffer struct {
    data []byte
}

// Requires constructor — zero value not safe; document this
// NewRateLimiter must be used; zero value of RateLimiter is not valid.
type RateLimiter struct {
    limit  int
    ticker *time.Ticker
}

func NewRateLimiter(limit int) *RateLimiter {
    return &RateLimiter{
        limit:  limit,
        ticker: time.NewTicker(time.Second),
    }
}
```

---

## Control Flow

### Early Returns & Guard Clauses

Mirror the Python principle: fail fast, keep the happy path unindented.

```go
// Bad — deeply nested
func processOrder(order *Order) error {
    if order != nil {
        if order.IsValid() {
            if order.HasItems() {
                // actual logic buried here
            }
        }
    }
    return nil
}

// Good — guard clauses
func processOrder(order *Order) error {
    if order == nil {
        return fmt.Errorf("processOrder: order is nil")
    }
    if !order.IsValid() {
        return fmt.Errorf("processOrder: invalid order %s", order.ID)
    }
    if !order.HasItems() {
        return fmt.Errorf("processOrder: order %s has no items", order.ID)
    }
    // happy path at top level
    return fulfil(order)
}
```

### Switch Over If-Else Chains

```go
// Bad
if status == "active" {
    handleActive()
} else if status == "pending" {
    handlePending()
} else if status == "cancelled" {
    handleCancelled()
}

// Good
switch status {
case "active":
    handleActive()
case "pending":
    handlePending()
case "cancelled":
    handleCancelled()
default:
    return fmt.Errorf("unknown status: %s", status)
}
```

---

## Concurrency

Go's concurrency primitives are powerful and easy to misuse. Follow these rules strictly.

### Core Rules

- **Document goroutine ownership.** Who starts it? Who stops it? What's its lifetime?
- **Always provide a cancellation path.** Pass `context.Context` as the first argument to any function that may block.
- **Never start a goroutine without knowing how it ends.**
- **Prefer channels for communication; mutexes for state protection.** Don't mix them without care.

```go
// Bad — goroutine with no cancellation, no lifecycle
go func() {
    for {
        process(fetchNext())
    }
}()

// Good — goroutine with context and clean shutdown
func startWorker(ctx context.Context, jobs <-chan Job) {
    go func() {
        for {
            select {
            case <-ctx.Done():
                return // clean exit
            case job, ok := <-jobs:
                if !ok {
                    return // channel closed
                }
                process(job)
            }
        }
    }()
}
```

### Context

```go
// Context is always the first parameter
func FetchUser(ctx context.Context, id string) (User, error) { ... }

// Respect cancellation
func longOperation(ctx context.Context) error {
    for i := 0; i < MAX_ITERATIONS; i++ {
        select {
        case <-ctx.Done():
            return ctx.Err()
        default:
        }
        // do work
    }
    return nil
}
```

### Race Conditions

Run tests with the race detector. Always.

```bash
go test -race ./...
```

---

## Power of 10 — Go Adaptation

### 1. Simple Control Flow

No `goto`. Avoid deeply nested goroutine fan-outs. Use iterative patterns; if recursion is needed, add an explicit depth guard.

```go
const maxDepth = 100

func traverse(node *Node, depth int) error {
    if depth > maxDepth {
        return fmt.Errorf("traverse: exceeded max depth %d", maxDepth)
    }
    if node == nil {
        return nil
    }
    if err := process(node); err != nil {
        return fmt.Errorf("traverse: node %s: %w", node.ID, err)
    }
    return traverse(node.Next, depth+1)
}
```

### 2. Fixed Loop Bounds

```go
const maxRetries = 10

for attempt := range maxRetries {
    err := doOperation()
    if err == nil {
        break
    }
    if attempt == maxRetries-1 {
        return fmt.Errorf("operation failed after %d attempts: %w", maxRetries, err)
    }
}
```

### 3. Bounded Data Structures

```go
// Bad — unbounded channel
jobs := make(chan Job)

// Good — buffered with explicit capacity
const maxQueueDepth = 500
jobs := make(chan Job, maxQueueDepth)

// Bounded cache with explicit eviction
import "github.com/hashicorp/golang-lru/v2"

cache, err := lru.New[string, User](1000)
if err != nil {
    return fmt.Errorf("init cache: %w", err)
}
```

### 4. Short Functions

Maximum ~50 lines. If a function needs more, extract helpers. A function that
handles both the happy path and three error cases is probably two functions.

### 5. High Assertion Density

Go doesn't have `assert` in production code, but the principle maps directly to **early validation and invariant checks**.

```go
func calculateAverage(values []float64) (float64, error) {
    // Preconditions
    if values == nil {
        return 0, fmt.Errorf("calculateAverage: values is nil")
    }
    if len(values) == 0 {
        return 0, fmt.Errorf("calculateAverage: values is empty")
    }

    total := 0.0
    for _, v := range values {
        total += v
    }
    result := total / float64(len(values))

    // Postcondition
    min, max := slices.Min(values), slices.Max(values)
    if result < min || result > max {
        return 0, fmt.Errorf("calculateAverage: result %f outside range [%f, %f]", result, min, max)
    }

    return result, nil
}
```

### 6. Minimal Variable Scope

Declare variables inside the block where they're needed. Use `:=` in the narrowest scope possible. Avoid package-level mutable state.

```go
// Bad — broad scope
var result string
if condition {
    result = "yes"
} else {
    result = "no"
}
use(result)

// Good — scoped to use site
result := "no"
if condition {
    result = "yes"
}
use(result)
```

### 7. Check All Return Values

The compiler enforces this for errors — don't subvert it.

```go
// Bad — discarding error
os.Remove(tmpFile)

// Good — handle or explicitly acknowledge
if err := os.Remove(tmpFile); err != nil {
    logger.Warn("failed to clean up temp file", "path", tmpFile, "err", err)
}
```

### 8. Limit Metaprogramming

Avoid `reflect` outside of framework-level code. Avoid `unsafe` entirely. If you find yourself reaching for `interface{}` / `any` pervasively, reconsider your design.

```go
// Bad — opaque, unanalyzable
func process(data interface{}) interface{} { ... }

// Good — concrete types or constrained generics
func process[T Processable](data T) (Result, error) { ... }
```

### 9. Limit Data Structure Nesting

Use structs with named fields instead of `map[string]map[string]interface{}`. Nested maps are a code smell.

```go
// Bad
config := map[string]map[string]interface{}{
    "database": {
        "host": "localhost",
        "port": 5432,
    },
}

// Good
type DatabaseConfig struct {
    Host string
    Port int
}

type Config struct {
    Database DatabaseConfig
}
```

### 10. Enable All Static Analysis

```yaml
# .golangci.yml
run:
  timeout: 5m

linters:
  enable:
    - govet
    - staticcheck
    - errcheck
    - gosimple
    - ineffassign
    - unused
    - gocyclo
    - misspell
    - godot
    - noctx
    - bodyclose
    - contextcheck
```

```bash
# In CI — fail on any lint warning
golangci-lint run --max-issues-per-linter=0 --max-same-issues=0
go test -race -coverprofile=coverage.out ./...
```

---

## Documentation

Go doc comments are parsed by `godoc` and `pkg.go.dev`. Format matters.

```go
// Package auth provides token-based authentication utilities.
// It supports JWT and opaque token formats and is safe for concurrent use.
package auth

// UserStore retrieves and persists user records.
// Implementations must be safe for concurrent use.
type UserStore interface {
    // FindByID returns the user with the given ID.
    // Returns ErrNotFound if no user exists with that ID.
    FindByID(ctx context.Context, id string) (User, error)
}

// ParseToken validates and decodes a JWT token string.
// It returns the claims contained in the token or an error
// if the token is expired, malformed, or has an invalid signature.
func ParseToken(tokenStr string, secret []byte) (*Claims, error) {
```

Rules:
- Comments on exported identifiers are **mandatory**.
- Start the comment with the name of the thing being documented.
- Full sentences ending with periods.
- Document concurrency safety on types that will be shared.

---

## Project Layout (General Purpose)

```
myproject/
├── cmd/
│   └── myapp/
│       └── main.go          # Entry point only — minimal logic here
├── internal/                # Private packages — not importable externally
│   ├── auth/
│   ├── store/
│   └── config/
├── pkg/                     # Public packages — safe for external import
│   └── httputil/
├── testdata/                # Test fixtures
├── go.mod
├── go.sum
├── .golangci.yml
└── Makefile
```

`main.go` should only wire dependencies and start the application. All logic lives in packages.

---

## Testing

```go
// test_<function>_<scenario> naming, same principle as Python
func TestFindByID_ReturnsUser(t *testing.T) { ... }
func TestFindByID_ReturnsErrNotFound(t *testing.T) { ... }
func TestFindByID_ReturnsErrorOnDBFailure(t *testing.T) { ... }

// Table-driven tests for multiple scenarios
func TestCalculateAverage(t *testing.T) {
    tests := []struct {
        name    string
        input   []float64
        want    float64
        wantErr bool
    }{
        {"single value", []float64{5}, 5.0, false},
        {"multiple values", []float64{1, 2, 3}, 2.0, false},
        {"empty slice", []float64{}, 0, true},
        {"nil slice", nil, 0, true},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := calculateAverage(tt.input)
            if (err != nil) != tt.wantErr {
                t.Errorf("wantErr=%v, got err=%v", tt.wantErr, err)
            }
            if got != tt.want {
                t.Errorf("want %f, got %f", tt.want, got)
            }
        })
    }
}
```

Always run: `go test -race -count=1 ./...`
