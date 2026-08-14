# `go run` vs `go build`

## `go run`
`go run` **compiles and runs the program in one step**.

Example:

```go
go run main.go
```

### What actually happens internally

1. Go compiler compiles `main.go`
    
2. It creates a **temporary binary**
    
3. The binary is executed
    
4. The binary is deleted after execution
    

Flow:

```go
 source code (.go)
      ↓
   compile
      ↓
temporary executable
      ↓
     run
      ↓
    delete
```

So `go run` is mainly for:

- development
    
- testing code quickly
    
- scripts

---
## `go build`

`go build` **compiles your program and creates a binary executable**.

Example:

```go
go build main.go
```

Result:

```bash
main.go  
main      ← compiled executable
```

Now you can run it like:

```bash
main.go
```

---

### Internal process

source code (.go)  
      ↓  
compile  
      ↓  
binary executable  
      ↓  
stored in directory

---

### Why backend developers use `go build`

Because you deploy **binaries**, not source code.

Example production workflow:

```go
write Go backend
      ↓
  go build
      ↓
upload binary to server
      ↓
  run service
```

Example:

```go
go build -o server // creates server
```


Run:
```go
./server
```

---

### Cross-compilation (very powerful in Go)

You can build binaries for **any OS**.

Example:

Linux binary:

```go
GOOS=linux GOARCH=amd64 go build
```

Mac binary:

```go
GOOS=darwin GOARCH=amd64 go build
```

This is why Go is heavily used in:

- backend services
    
- DevOps tools
    
- cloud infrastructure
    

(Kubernetes, Docker CLI, Terraform are written in Go)


---

# Go Project Structure

Go has a **very opinionated structure** that makes projects scalable.

A simple backend project might look like:

```go
myapp/
│
├── go.mod
├── go.sum
│
├── cmd/
│   └── server/
│       └── main.go
│
├── internal/
│   ├── handler/
│   │   └── user_handler.go
│   │
│   ├── service/
│   │   └── user_service.go
│   │
│   └── repository/
│       └── user_repo.go
│
├── pkg/
│   └── utils/
│       └── helper.go
│
└── configs/
    └── config.go
```

Let's break this down.

---

## `main.go`

Entry point of program.

Example:

```go
package main

import "fmt"

func main() {
    fmt.Println("Server started")
}
```

Go programs must start from package main.

---
## `cmd/`

Contains **entry points for applications**.

Example:

```go
cmd/
  api/
    main.go
  worker/
    main.go
```

This allows multiple services.

Example:

```go
go run cmd/api/main.go
```

---
## `internal/`

Code that **cannot be imported outside the project**.

Example:

```go
internal/
    database/
    auth/
    service/
```

If another project tries:

```go
import myapp/internal/auth
```

Go **won't allow it**.

This protects internal business logic.

Backend teams rely heavily on this.

---
## `pkg/`

Reusable packages that **can be used by other projects**.

Example:

```go
pkg/  
   logger/  
   utils/
```

Used for shared libraries.

---
## `configs/`

Configuration management.

Example:

```go
configs/
    config.go
```

Typical content:

```go
read environment variables
database credentials
server ports
```


---
## `go.mod`

This file defines:

- project module
- dependencies

Example:

```go
module github.com/username/myapp

go 1.22

require (
    github.com/gin-gonic/gin v1.9.0
)
```

### `go mod` (Modules System)

Before Go modules existed, Go used **GOPATH** which was messy.

Modules solve:

- dependency management
    
- versioning
    
- reproducible builds
    

---

## Initialize module

```go
go mod init github.com/username/myapp
```

Creates:

```go
go.mod
```

Example:

```go
module github.com/username/myapp

go 1.22
```

This tells Go:

> This project is a module named `github.com/username/myapp`.

---

## Installing dependencies

Example:

```go
go get github.com/gin-gonic/gin
```

Result:

`go.mod`

```go
require github.com/gin-gonic/gin v1.9.0
```

And `go.sum` gets created.

---
## `go.sum`

This file stores **checksums for dependencies**.

Example:

```go
github.com/gin-gonic/gin v1.9.0 h1:abcxyz...
```

Purpose:

- security
- integrity verification

Ensures dependency code **has not been modified**.

---
## Dependency resolution

When you run:

```go
go build
```

Go:

1. Reads `go.mod`
    
2. Downloads dependencies
    
3. Stores them in cache
    

Location:

```go
$GOPATH/pkg/mod
```

Example path:

```go
~/go/pkg/mod
```


---

## Useful `go mod` commands

### Download dependencies

```go
go mod download
```

---

### Clean unused dependencies

```go
go mod tidy
```

Removes unused packages.

---

### Verify dependencies

go mod verify

Checks integrity.

```go
go mod verify
```
---

### Vendor dependencies

```go
go mod vendor
```

Copies dependencies locally.
Used in some production environments.

---
# How these pieces connect (Real backend workflow)

Example backend workflow:

### 1️⃣ Create project

```go
mkdir go-api  
cd go-api
```

---

### 2️⃣ Initialize module

```go
go mod init github.com/user/go-api
```

---

### 3️⃣ Create main file

```go
main.go
```

Example:

```go
package main

import "fmt"

func main() {
    fmt.Println("API server running")
}
```

___
### 4️⃣ Run during development

```go
go run main.go
```

---

### 5️⃣ Build for deployment

```go
go build -o server
```

---

### 6️⃣ Deploy binary

```go
./server
```



Think of Go like this:

```go
module  
   ↓  
packages  
   ↓  
files  
   ↓  
functions
```

Example:

```go
module: github.com/user/api

package: user

file: user.go

function: CreateUser()
```


# One thing backend devs MUST understand early

In Go:

**everything revolves around packages**

Example import:
```go
import "fmt"
```

This imports the **fmt package**.

Your project will also be split into packages.

Example:

```go
import "myapp/internal/service"
```