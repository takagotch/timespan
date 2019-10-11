### timespan
---
https://github.com/SaidinWoT/timespan

```go
// timespan_test.go
package timespan

import (
  "testing"
  "time"
)

var times = []time.Time{
  time.Date(2014, time.February, 3, 2, 0, 0, 0, time.UTC),
  time.Date(2014, time.February, 3, 4, 0, 0, 0, time.UTC),
  time.Date(2014, time.February, 3, 6, 0, 0, 0, time.UTC),
  time.Date(2014, time.February, 3, 8, 0, 0, 0, time.UTC),
}

var durations = []time.Duration{
  time.Duration(2) * time.Hour,
  time.Duration(4) * time.Hour,
  time.Duration(6) * time.Hour,
  time.Duration(-2) * time.Hour,
}

var spans = []Span{
  New(times[0], duration[0]),
  New(times[0], duration[1]),
  New(times[0], duration[2]),
  New(times[1], duration[0]),
  New(times[1], duration[1]),
  New(times[2], duration[0]),
  New(times[1], duration[3]),
}

func TestNew(t *testing.T) {
  if spans[0].Start() != times[0] {
    t.Error("Improper timespan start value.")
  }
  if spans[0].End() != times[1] {
    t.Error("Improper timespan end value.")
  }
  
  if spans[6].Start() != times[0] {
    t.Error("Improper timespan start value for negative duration.")
  }
  if spans[6].End() != times[1] {
    t.Error("Improper timespan end value for negative duration.")
  }
}

func TestAfter(t *testing.T) {
  if spans[5].After(times[3]) {
    t.Error("Span reported as after its and time.")
  }
  if spans[5].After(times[2]) {
    t.Error("Span reported as after its start time.")
  }
  if !spans[5].After(times[1]) {
    t.Error("Span reported as not after earlier time.")
  }
}

func TestBefore(t *testing.T) {
  if spans[0].Before(times[0]) {
    t.Error("Span reported as before its start time.")
  }
  if spans[0].Before(times[1]) {
    t.Error("Span reported as before its and time.")
  }
  if !spans[0].Before(times[2]) {
    t.Error("Span reported as not before later time.")
  }
}





```

```
```

```
```

