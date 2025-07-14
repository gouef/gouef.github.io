<img align=right width="168" src="docs/gouef_logo.png">

# prime-numbers
Prime numbers, you can Validate, get list or get multiply table.

[![Static Badge](https://img.shields.io/badge/Github-gouef%2Fprime--numbers-blue?style=for-the-badge&logo=github&link=github.com%2Fgouef%2Fprime-numbers)](https://github.com/gouef/prime-numbers)

[![GoDoc](https://pkg.go.dev/badge/github.com/gouef/prime-numbers.svg)](https://pkg.go.dev/github.com/gouef/prime-numbers)
[![GitHub stars](https://img.shields.io/github/stars/gouef/prime-numbers?style=social)](https://github.com/gouef/prime-numbers/stargazers)
[![Go Report Card](https://goreportcard.com/badge/github.com/gouef/prime-numbers)](https://goreportcard.com/report/github.com/gouef/prime-numbers)
[![codecov](https://codecov.io/github/gouef/prime-numbers/branch/main/graph/badge.svg?token=YUG8EMH6Q8)](https://codecov.io/github/gouef/prime-numbers)

## Versions
![Stable Version](https://img.shields.io/github/v/release/gouef/prime-numbers?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/prime-numbers?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/prime-numbers?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)

## Features

- Validate number if it's a prime number.
- Generate list of prime numbers (by size).
- Create Multiply table of prime numbers.

## Installation

```shell
go get -u github.com/gouef/prime-numbers
```

## Usages

### Validate
function Validate returns bool.

```go
package main

import (
	"log"
	primeNumbers "github.com/gouef/prime-numbers"
)

func main() {
	num := 13
	isPrime := primeNumbers.Validate(num)
	if isPrime == false {
		log.Fatalf("Number : %v is not a prime number", num)
	}
}

```



### Generator
function Generator returns []int of prime numbers.

```go
package main

import (
	"log"
	primeNumbers "github.com/gouef/prime-numbers"
)

func main() {
	size := 3
	listPrimeNumbers := primeNumbers.Generate(size) // returns []int{2, 3, 5}
	
	if len(listPrimeNumbers) == 3 {
		// ...
    }
}

```



### MultiplyTable
function MultiplyTable returns map[int]map[int]int of prime numbers.

```go
package main

import (
	"log"
	primeNumbers "github.com/gouef/prime-numbers"
)

func main() {
	size := 3
	numberTable := primeNumbers.MultiplyTable(size) 
	// returns map[int]map[int]int{
	//  2: {2: 4, 3: 6, 5: 10},
	//  3: {2: 6, 3: 9, 5: 15},
	//  5: {2: 10, 3: 15, 5: 25},
    // }

	for i1, l := range numberTable {
		for i2, m := range l {
            log.Printf("Number %v x %v = %v", i1, i2, m)
		}
	}
}

```


## Contributing

Read [Contributing](CONTRIBUTING.md)

## Contributors

<div>
<span>
  <a href="https://github.com/JanGalek"><img src="https://raw.githubusercontent.com/gouef/prime-numbers/refs/heads/contributors-svg/.github/contributors/JanGalek.svg" alt="JanGalek" /></a>
</span>
<span>
  <a href="https://github.com/actions-user"><img src="https://raw.githubusercontent.com/gouef/prime-numbers/refs/heads/contributors-svg/.github/contributors/actions-user.svg" alt="actions-user" /></a>
</span>
</div>

## Join our Discord Community! 🎉

[![Discord](https://img.shields.io/discord/1334331501462163509?style=for-the-badge&logo=discord&logoColor=white&logoSize=auto&label=Community%20discord&labelColor=blue&link=https%3A%2F%2Fdiscord.gg%2FwjGqeWFnqK
)](https://discord.gg/wjGqeWFnqK)

Click above to join our community on Discord!
