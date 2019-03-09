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

```
```

```
```


