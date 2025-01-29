<img align=right width="168" src="docs/gouef_logo.png">

# Country
This package provides functions to search for country information ([ISO 3166-1](https://www.iso.org/iso-3166-country-codes.html)) based on their country codes (Alpha-2, Alpha-3, Numeric) and names. It is designed for easy integration into applications that need to work with country codes or names.


[![Static Badge](https://img.shields.io/badge/Github-gouef%2Fcountry-blue?style=for-the-badge&logo=github&link=github.com%2Fgouef%2Fcountry)](https://github.com/gouef/country)

[![GoDoc](https://pkg.go.dev/badge/github.com/gouef/country.svg)](https://pkg.go.dev/github.com/gouef/country)
[![GitHub stars](https://img.shields.io/github/stars/gouef/country?style=social)](https://github.com/gouef/country/stargazers)
[![Go Report Card](https://goreportcard.com/badge/github.com/gouef/country)](https://goreportcard.com/report/github.com/gouef/country)
[![codecov](https://codecov.io/github/gouef/country/branch/main/graph/badge.svg?token=YUG8EMH6Q8)](https://codecov.io/github/gouef/country)

## Versions
![Stable Version](https://img.shields.io/github/v/release/gouef/country?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/country?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/country?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)

## Installation

To use this package in your project, add it using Go modules:

```bash
go get -u github.com/gouef/country
```

## Usage
`Country` **Struct**
Each country is represented by the `Country` struct, which contains the following fields:

- `Name`: The country's name (in English).
- `Alpha2`: The two-letter country code (ISO 3166-1 alpha-2).
- `Alpha3`: The three-letter country code (ISO 3166-1 alpha-3).
- `Numeric`: The numeric country code (ISO 3166-1 numeric).

## Functions

`FindByAlpha2(alpha2 string) *Country`

This function searches for a country by its two-letter Alpha-2 code.

```go
package main

import "github.com/gouef/country"

sCountry := country.FindByAlpha2("CZ")
if sCountry != nil {
    fmt.Println("Country Name:", sCountry.Name)
    fmt.Println("Alpha-2 Code:", sCountry.Alpha2)
}
```

`FindByAlpha3(alpha3 string) *Country`

This function searches for a country by its three-letter Alpha-3 code.

```go
package main

import "github.com/gouef/country"

sCountry := country.FindByAlpha3("CZE")
if sCountry != nil {
    fmt.Println("Country Name:", sCountry.Name)
    fmt.Println("Alpha-3 Code:", sCountry.Alpha3)
}
```

`FindByName *Country`

This function searches for a country by its name (english).

```go
package main

import "github.com/gouef/country"

sCountry := country.FindByName("Czechia")
if sCountry != nil {
    fmt.Println("Country Name:", sCountry.Name)
    fmt.Println("Alpha-2 Code:", sCountry.Alpha2)
    fmt.Println("Alpha-3 Code:", sCountry.Alpha3)
}
```

## Example

```go
package main

import (
	"fmt"
	"github.com/gouef/country"
)

func main() {
	// Search by Alpha-2 code
	sCountry := country.FindByAlpha2("CZ")
	if sCountry != nil {
		fmt.Println("Found country:", sCountry.Name)
	}

	// Search by Alpha-3 code
	sCountry = country.FindByAlpha3("CZE")
	if sCountry != nil {
		fmt.Println("Found country:", sCountry.Name)
	}

	// Search by name
	sCountry = country.FindByName("Czechia")
	if sCountry != nil {
		fmt.Println("Found country:", sCountry.Name)
	}
}

```

## Contributing

Read [Contributing](CONTRIBUTING.md)

## Contributors

<div>
<span>
  <a href="https://github.com/JanGalek"><img src="https://raw.githubusercontent.com/gouef/country/refs/heads/contributors-svg/.github/contributors/JanGalek.svg" alt="JanGalek" /></a>
</span>
<span>
  <a href="https://github.com/actions-user"><img src="https://raw.githubusercontent.com/gouef/country/refs/heads/contributors-svg/.github/contributors/actions-user.svg" alt="actions-user" /></a>
</span>
</div>

