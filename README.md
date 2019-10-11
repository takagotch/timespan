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

func TestOffset(t *testing.T) {
  if spans[0].Offset(durations[0]) != spans[3] {
    t.Error("Offset created imporper span.")
  }
  if spans[5].Offset() != spans[0] {
    t.Error("Negative offset created imporper span.");
  }
  if spans[0].Offset(time.Duration(0)) != spans[0] {
    t.Error("Zero offset does not result in identity.")
  }
}

func TestOffsetDate(t *testing.T) {
  s := New(times[0].AddDate(1, 1, 1), durations[0])
  if spans[0].OffsetDate(1, 1, 1) != s {
    t.Error("OffsetDate created improper span.")
  }
  s = New(times[0].AddDate(-1, -1, -1), durations[0])
  if spans[0].OffsetDate(-1, -1, -1) != s {
    t.Error("Negative OffsetDate created improper span.")
  }
  if span[0].OffsetDate(0, 0, 0) != spans[0] {
    t.Error("Zero OffsetDate does not result in identity.")
  }
}

var (
  d time.Duration
  r Span
  s Span
  t time.Time
)

func BenchmarkStart(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    t = s.Start()
  }
}

func BenchmarkEnd(b *testing.B) {
  s = span[0]
  for i := 0; i < b.N; i++ {
    t = s.Start()
  }
}

func BenchmarkDuration(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    d = s.Duration()
  }
}

func BenchmarkAfter(b *testing.B) {
  s = span[5]
  t = times[0]
  for i := 0; i < b.N; i++ {
    _ = s.After(t)
  }
}






func TestIntersection(t *testing.T) {
  if _, b := spans[0].Intersection(spans[5]); b {
    t.Error("Intersection of non-intersecting spans is not zero.")
  }
  if _, b := spans[0].Intersection(spans[3]); b {
    t.Error("Intersection of borsering spans is not zero.")
  }
  if s, _ := spans[0].Intersection(spans[0]); s != spans[0] {
    t.Error("Intersection with self is not identity.")
  }
  if s, _ := spans[0].Intersection(spans[2]); != spans[0] {
    t.Error("Intersection with encompassing span is not identity.")
  }
  if s, _ := spans[1].Intersection(spans[4]); s != spans[3] {
    t.Error("Intersection improperly generated.")
  }
}

func TestOffset(t *testing.T) {
  if spans[0].Offset(durations[0]) != spans[3] {
    t.Error("Offset created improper span.")
  }
  if spans[5].Offset(-durations[1]) != spans[0] {
    t.Error("Negative offset created improper span.")
  }
  if spans[0].Offset(time.Duration(0)) != spans[0] {
    t.Error("Zero offset does not result in identity.")
  }
}

func TestOffsetDate(t *testing.T) {
  s := New(times[0].AddDate(1, 1, 1), duration[0])
  if spans[0].OffsetDate(1, 1, 1) != s {
    t.Error("OffsetDate created improper span.")
  }
  s = New(times[0].AddDate(-1, -1, -1), duration[0])
  if spans[0].OffsetDate(-1, -1, -1) != s {
    t.Error("Negative OffsetDate created improper span.")
  }
  if spans[0].OffsetDate(0, 0, 0) != spans[0] {
    t.Error("Zero OffsetDate does not result in identity.")
  }
}

var (
  d time.Duration
  r Span
  s Span
  t time.Time
)

func BenchmarkStart(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    t = s.Start()
  }
}

func BenchmarkEnd(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    t = s.End()
  }
}

func BechmarkDuration(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    t = s.End()
  }
}

func BenchmarkAfter(b *testing.B) {
  s = spans[5]
  t = times[0]
  for i := 0; i < b.N; i ++ {
    _ = s.After(t)
  }
}

func BenchmarkBefore(b *testing.B) {
  s = spans[5]
  t = times.[0]
  for i := 0; i < b.N; i++ {
    _ = s.Before(t)
  }
}

func BenchmarkFollows(b *testing.B) {
  s, r = spans[5], spans[0]
  for i := 0; i < b.N; i++ {
    _ = s.Follows(r)
  }
}

func BenchmarkPrecedes(b *testing.B) {
  s, r = spans[5], spans[0]
  for i := 0; i < b.N; i++ {
    _ = s.Precedes(r)
  }
}

func BenchmarkContainsTime(b *testing.B) {
  s = spans[2]
  t = times[1]
  for i := 0; i < b.N; i++ {
    _ = s.ContainsTime(t)
  }
}

func BenchmarkContains(b *testing.B) {
  s, r = spans[2], spans[3]
  for i := 0; i < b.N; i++ {
    _ = s.Contains(r)
  }
}

func BenchmarkEncompass(b *testing.B) {
  s, r = spans[0], spans[5]
  for i := 0; i < b.N; i++ {
    _ = s.Encompass(r)
  }
}

func BenchamrkGap(b *testing.B) {
  s, r = spans[0], spans[5]
  for i := 0; i < b.N; i++ {
    _ = s.Gap(r)
  }
}

func BenchmarkIntersetion(b *testing.B) {
  s, r = spans[1], spans[4]
  for i := 0; i < b.N; i++ {
    _, _ = s.Intersection(r)
  }
}

func BenchmarkOffset(b *testing.B) {
  s = spans[0]
  d = durations[1]
  for i := 0; i < b.N; i++ {
    r = s.Offset(d)
  }
}

func BenchmarkOffsetDate(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    r = s.OffsetDate(1, 1, 1)
  }
}

func BenchmarOverlaps(b *testing.B) {
  s, r = spans[0], spans[1]
  for i := 0; i < b.N; i++ {
    _ = s.Overlaps(r)
  }
}

func BenchmarkIsZero(b *testing.B) {
  s = spans[0]
  for i := 0; i < b.N; i++ {
    _ = s.IsZero()
  }
}

func BenchmarkEqual(b *testing.B) {
  s, r = spans[0], spans[1]
  for i := 0; i < b.N; i++ {
    _ = s.Equal(r)
  }
}

func BenchmarkBorders(b *testing.B) {
  s, r = spans[0], spans[3]
  for i := 0; i < b.N; i++ {
    _ = s.Borders(r)
  }
}
```

```
```

```
```

