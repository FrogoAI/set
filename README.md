# Go Generic Set

A simple, lightweight, and type-safe implementation of `Set` data structures in Go, built with generics.

This repository provides two common set implementations: a standard unordered set for high performance and an ordered set that preserves the insertion order of elements.

## ✨ Features

- **Type-Safe & Generic**: Built using Go 1.18+ generics, it works with any `comparable` type (e.g., `string`, `int`, `float64`).
- **Two Implementations**:
    - `GenericDataSet`: An unordered set optimized for fast `O(1)` lookups, additions, and deletions.
    - `GenericOrderedDataSet`: An ordered set that maintains the original insertion order of its elements.
- **Core Set API**: Provides essential methods like `Add`, `Delete`, `Contains`, `Union` (for unordered sets), `Count`, and `ToSlice`.
- **Well-Tested**: Includes a comprehensive suite of unit and fuzz tests to ensure reliability.
- **Lightweight**: Zero external dependencies.

------

## 🚀 Installation

Bash

```
go get github.com/your-username/go-generic-set
```

------

## 💡 Usage

### Unordered Set (`GenericDataSet`)

Use this when you need maximum performance for membership testing and don't care about the order of elements.

```
package main

import (
	"fmt"
	
	"github.com/FrogoAI/set"
)

func main() {
	// Create a new set of integers
	s1 := set.NewGenericDataSet(1, 2, 3, 3, 4)

	// Add an element
	s1.Add(5)

	// Test for membership
	fmt.Printf("Set contains 3: %v\n", s1.Contains(3)) // true
	fmt.Printf("Set contains 99: %v\n", s1.Contains(99)) // false

	// Perform a union operation
	s2 := set.NewGenericDataSet(5, 6, 7)
	s1.Union(s2)

	// Convert to a slice (order is not guaranteed)
	fmt.Println("Slice:", s1.ToSlice()) // e.g., [1 2 3 4 5 6 7]
	fmt.Println("Count:", s1.Count())   // 7
}
```

### Ordered Set (`GenericOrderedDataSet`)

Use this when you need to preserve the order in which elements were added to the set.

```
package main

import (
	"fmt"
	"github.com/your-username/go-generic-set/set"
)

func main() {
	// Create a new ordered set of strings
	orderedSet := set.NewGenericOrderedDataSet("apple", "banana", "cherry")

	// Adding a duplicate element does not change the order
	orderedSet.Add("banana")

	// Add a new element
	orderedSet.Add("date")

	// Delete an element
	orderedSet.Delete("banana")
    
	// Get the last element
	fmt.Println("Last element:", orderedSet.Last()) // date

	// The slice preserves the original insertion order
	// Output: [apple cherry date]
	fmt.Println("Ordered Slice:", orderedSet.ToSlice()) 
}
```

