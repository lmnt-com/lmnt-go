# LMNT Go SDK

The LMNT Go SDK provides convenient access to the [LMNT API](https://docs.lmnt.com/api/) from Go applications.

## Documentation

Full documentation is available at [docs.lmnt.com/api/sdks/go](https://docs.lmnt.com/api/sdks/go).

## Installation

```sh
go get github.com/lmnt-com/lmnt-go
```

## Getting started

```go
package main

import (
	"context"
	"io"
	"os"

	lmnt "github.com/lmnt-com/lmnt-go"
	"github.com/lmnt-com/lmnt-go/option"
)

func main() {
	client := lmnt.NewClient(
		option.WithAPIKey(os.Getenv("LMNT_API_KEY")), // This is the default and can be omitted
	)

	response, err := client.Speech.Generate(context.TODO(), lmnt.SpeechGenerateParams{
		Text:  "hello world.",
		Voice: "leah",
	})
	if err != nil {
		panic(err)
	}
	defer response.Body.Close()

	out, _ := os.Create("speech.mp3")
	defer out.Close()
	io.Copy(out, response.Body)
}
```

## Requirements

Go 1.23 or later is supported.
