### go-fuzz
---
https://github.com/dvyukov/go-fuzz

```go
func Fuzz(data []byte) int

package png

import (
  "bytes"
  "image/png"
)

func Fuzz(data []byte) int {
  png.Decode(bytes.NewReader(data))
  return 0
}


func Fuzz(data []byte) int {
  img, err := png.Decode(bytes.NewReader(data))
  if err != nil {
    if img != nil {
      panic("img != nil or error")
    }
    return 0
  }
  var w bytes.Buffer
  err = png.Encode(&w, img)
  if err != nil {
    panic(err)
  }
  return 1
}
```

```sh
go get -u github.com/dvyukov/go-fuzz/...

go get -d github.com/dvyukov/go-fuzz-corpus
cd $GOPATH/src/github.com/dvyukov/go-fuzz-corpus
cd png
go-fuzz-build

go-fuzz

go-fuzz -workdir=examples/png -coordinator=127.0.0.1:8745
go-fuzz -bin=./png-fuzz.zip -worker=127.0.0.1:8745 -procs=10
```

```
```


