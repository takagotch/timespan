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



```

```
```

```
```

