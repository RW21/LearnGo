# Learn-Go

A personal Golang note.

# Assignment

## `:=` vs `var`

```go
package main

var toplevel = "Hello world"         // var keyword is required

func F() {
        withinBlock := "Hello world" // var keyword is not required
}
```

`var` used only outside of block.

# Array

# Slices

Slices are references to an array.

## Using `make` to create slices

Used to create dynamic arrays. `a := make([]int, 5)` will be `[0 0 0 0 0]`.

## Iterate through a slice



# Flow Control

## loops

```GO
func main() {
    // 普通のforの繰り返し
    for i := 0; i < 10; i++ {
        if i == 3 {
            continue
        } else if i == 8 {
            break
        }

        fmt.Println(i)

    }

    // while文的にも作成可能
    n := 0
    for n < 10 {
        fmt.Println(n)
        n++
    }
}
```

### Slices and loops

```go
package main

import "golang.org/x/tour/pic"

func Pic(dx, dy int) [][]uint8 {
	image := make([][]uint8, dy)
	
	for i := range image{
		image[i] = make([]uint8, dx)	
	}
	
	for y:=0; y<dy; y++ {
		for x:=0; x<dx; x++{
			image[x][y] = uint8(x^y)	
		}
	}
	
	return image
}

func main() {
	pic.Show(Pic)
}
```

# Maps

```go
package main

import "fmt"

type Vertex struct {
	Lat, Long float64
}

var m map[string]Vertex

func main() {
	m = make(map[string]Vertex)
	m["Bell Labs"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["Bell Labs"])
}
```

## Test if element exists

Test that a key is present with a two-value assignment:

`elem, ok = m[key]`
If key is in m, ok is true. If not, ok is false.

## Iterate through map

```go
package main

import "fmt"

func main() {
    type Map1 map[string]interface{}
    type Map2 map[string]int
    m := Map1{"foo": Map2{"first": 1}, "boo": Map2{"second": 2}}
    //m = map[foo:map[first: 1] boo: map[second: 2]]
    fmt.Println("m:", m)
    for k, v := range m {
        fmt.Println("k:", k, "v:", v)
    }
}
```

## Iterate through string using map

```go
package main

import (
	"golang.org/x/tour/wc"
	"strings"
)

func WordCount(s string) map[string]int {
	m := make(map[string]int)
	for _, item := range strings.Fields(s){
	    m[item]++	
	}
	return m
}

func main() {
	wc.Test(WordCount)
}
```

# Functions

## Functions as values

```go
package main

import (
	"fmt"
	"math"
)

func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}

func main() {
	hypot := func(x, y float64) float64 {
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(5, 12))

	fmt.Println(compute(hypot))
	fmt.Println(compute(math.Pow))
}
```

## Function closure

```go
package main

import "fmt"

func adder() func(int) int {
	sum := 0
	return func(x int) int {
		sum += x
		return sum
	}
}

func main() {
	pos, neg := adder(), adder()
	for i := 0; i < 10; i++ {
		fmt.Println(
			pos(i),
			neg(-2*i),
		)
	}
}
```

### Fibonacci

```go
package main

import "fmt"

// fibonacci is a function that returns
// a function that returns an int.
func fibonacci() func() int {
	a, b := 0, 1
	return func() int {
		a, b = b, a+b
		return a
	}
}
s
func main() {
	f := fibonacci()
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}
```

# References
- https://stackoverflow.com/questions/8018719/iterating-through-a-golang-map
- https://stackoverflow.com/questions/21657446/var-vs-in-go
- https://stackoverflow.com/questions/31064688/which-is-the-nicer-way-to-initialize-a-map-in-golang
- 