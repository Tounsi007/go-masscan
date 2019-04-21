# go-masscan

go-masscan is a golang library to run masscan scans, parse scan results.


## Installation


```sh
go get github.com/lc/go-masscan
```
to install the package

```go
import "github.com/lc/go-masscan"
```

## Example

```go
package main

import (
	"github.com/lc/go-masscan"
	"fmt"
)

func main() {

	m := masscan.New()

	// masscan system path
	//m.SetSystemPath("/usr/local/masscan/bin/masscan")

	// port(s) to scan
	m.SetPorts("0-65535")

	// IP Range to scan
	m.SetRanges("0.0.0.0/8")

	// masscan rate
	m.SetRate("2000")

	// IP to exclude from scan.
	m.SetExclude("127.0.0.1")

	// Start Scan
	err := m.Run()
	if err != nil {
		log.Fatalf("Error running scan: %v", err)
		return
	}

	// Parse masscan results.
	results, err := m.Parse()
	if err != nil {
		log.Fatalf("Error parsing scan: %v",err)
		return
	}

	for _, result := range results {
		fmt.Println(result)

	}

}

```