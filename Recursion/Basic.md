## Basic of Recursion

Recursion is a programming concept where a function calls itself in its own definition. In other words, it is a process in which a function solves a problem by solving smaller instances of the same problem. The concept of recursion is often applied when a problem can be broken down into smaller, simpler subproblems.

Key features of recursion include:

1. **Base Case:**
   - Every recursive algorithm must have a base case, a condition that stops the recursion. The base case provides a solution directly without further recursive calls.

2. **Divide and Conquer:**
   - Recursion often involves breaking a problem into smaller subproblems of the same type. Each recursive call works on a smaller instance of the original problem.

3. **Function Calls Itself:**
   - The defining characteristic of recursion is that a function calls itself during its execution.

### Go Environment

```
src
|__ pkg3
|  |__ basic.go
|  |__ factorial.go
|  |__ ...
|__ main.go

# go mod init example.com/dmanish
# go mod edit -replace example.com/dmanish/pkg3=./pkg3
# go mod tidy
```

**Go main**
```go
package main

import subseq "example.com/dmanish/pkg3"

func main(){
	// fmt.Println("Welcome to DSA")
	subseq.Basic()
	// subseq.IsPalindrome()
	// subseq.GetFactorial()
	// subseq.SumOfn()
	// subseq.ReverseArray()
	// subseq.GetFibonacci()
	// subseq.SubSeq()
	// subseq.SubSeqSum()
	// subseq.MergSortAlgorithm()
	// subseq.CombinationSum()
	// subseq.QuickSort()
	// subseq.CombinationSum2()
	// subseq.SubSetSum1()
	// subseq.SubSetSum2()
}
```

**Basic.go**
```go
package subseq

func Basic(){
	...
}
```

**CombinationSum.go**
```go
pakcage subseq

func CombinationSum(){
	...
}
```
### Code

**Print name 5 times**
```go
package subseq

import "fmt"

func Basic() {
	fmt.Println("Tutorial Basic")
	printName(1, 5)
}

// Print name 5 times
func printName(i int, n int) {
	if i > n {
		return
	}

	fmt.Println("dmanis")
	printName(i+1, n)
}
```

**Print linearly from 1 to 10**
```go
package subseq

import "fmt"

func Basic() {
	fmt.Println("Tutorial Basic")
	printLinearly(1, 10)
}

// Print linearly from 1 to 10
func printLinearly(i int, n int) {
	if i > n {
		return
	}

	fmt.Println(i)
	printLinearly(i+1, n)

}
```

**Print from N to 1**
```go
package subseq

import "fmt"

func Basic() {
	fmt.Println("Tutorial Basic")
	printLinearlyRev(10, 1)
}

// Print from N to 1
func printLinearlyRev(n int, i int) {
	if i > n {
		return
	}

	fmt.Println(n)
	printLinearlyRev(n-1, i)

}
```

**Print linearly from 1 to N (using backtrack)**
```go
package subseq

import "fmt"

func Basic() {
	fmt.Println("Tutorial Basic")
	n := 10
	printLinearlyBacktrack(n, n)
}

// Print linearly 1 to N (using backtrack)
func printLinearlyBacktrack(i int, n int) {
	if i < 1 {
		return
	}

	printLinearlyBacktrack(i-1, n)
	fmt.Println(i)

}
```

**Print from N to 1 (using backtrack)**
```go
package subseq

import "fmt"

func Basic() {
	fmt.Println("Tutorial Basic")
	n := 10
	printLinearlyRevBacktrack(1, n)
}

// Print from N to 1 (using backtrack)
func printLinearlyRevBacktrack(i int, n int) {
	if i > n {
		return
	}

	printLinearlyRevBacktrack(i+1, n)
	fmt.Println(i)

}
```